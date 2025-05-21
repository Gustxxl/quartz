tags: [[GLPI]] [[Десна]] [[IT, Information technology]] [[Linux]] [[Debian]]
___
1. Подключение по ssh
```bash
ssh bvi@10.1.0.19
```
password: ||777666||

2. Команды для определения версии Debian
```bash
lsb_release -a
```
или
```bash
cat /etc/os-release
```
или
```bash
uname -a
```

3. Изменение пароля
```bash
passwd
```

3. Обновление Debian до последней версии

> [!Важно]
> apt upgrade -y безопаснее, чем apt full-upgrade -y, потому что ничего не удаляет и не меняет зависимости.
> Однако даже с -y может быть риск при обновлении критичных пакетов, нужно проверять заранее что обновляется.

Обновляет список доступных пакетов (из bookworm-репозиториев)
```bash
sudo apt update
```

Обновляет все уже установленные пакеты, если это возможно без удаления чего-либо (-y отвечает за автосоглашение)
```bash
sudo apt upgrade -y
```

Обновляет всё, даже если нужно что-то удалить или заменить. Это “глубокое” обновление.
```bash
sudo apt full-upgrade
```

Удаляет ненужные (больше не используемые) зависимости и пакеты.
```bash
sudo apt autoremove
```

Перезагрузка, чтобы применить обновления (если, например, обновилось ядро или systemd).
```bash
sudo reboot
```

4. Чек-лист для установки GLPI Проверка уже установленного софта роверка уже установленного софта

Для установки GLPI понадобятся:

- Веб-сервер
- PHP
- СУБД: MySQL/MariaDB
- GLPI: сам дистрибутив с оф. сайта

5. Проверка уже установленного софта
Веб-сервер: Apache/Nginx
```bash
apache2 -v
```

```bash
php -v
```

```bash
mysql --version
```
или (в зависимости от желаемой базы)
```bash
mariadb --version
```

6. Создание базы данных GLPI
   Пример на MariaDB:
   
   Входим в консоль MariaDB:
```bash
sudo mariadb
```

Команда для создания БД (Выполнять по одной строке):
```sql
-- Создание базы
CREATE DATABASE glpi_db DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

-- Создание пользователя для этой базы
CREATE USER 'glpi_user'@'localhost' IDENTIFIED BY 'myStrongPassword123';

-- Выдача пользователю прав на работу с БД
GRANT ALL PRIVILEGES ON glpi_db.* TO 'glpi_user'@'localhost';

-- Применение настроек
FLUSH PRIVILEGES;

-- Выход (можно и Ctrl+D)
EXIT;
```
За пример взяты:
Имя базы данных: glpi_db
Имя пользователя: glpi_user
Пароль: myStrongPassword123

"Шпаргалка"
```sql
-- Список всех баз
SHOW DATABASES;

-- Удалить лишнюю базу
DROP DATABASE название_базы;

-- Список всех пользователей
SELECT User, Host FROM mysql.user;

-- Удалить пользователя
DROP USER 'имя_пользователя'@'localhost';
```

7. Установка GLPI 15 версии (для последующего обновления)
```bash
cd /tmp

wget https://github.com/glpi-project/glpi/releases/download/10.0.15/glpi-10.0.15.tgz

tar -xvzf glpi-10.0.15.tgz

sudo mv glpi /var/www/html/

sudo chown -R www-data:www-data /var/www/html/glpi

sudo chmod -R 755 /var/www/html/glpi
```

8. Настройка Apache

Переходим в каталог с конфигами Apache
```bash
cd /etc/apache2/sites-available/
```

Создаем новый конфиг через nano
```bash
sudo nano glpi.conf
```

Сам конфиг
```apache
<VirtualHost *:80>
    ServerAdmin admin@example.com
    DocumentRoot /var/www/html/glpi

    <Directory /var/www/html/glpi>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/glpi_error.log
    CustomLog ${APACHE_LOG_DIR}/glpi_access.log combined
</VirtualHost>
```

В nano:
Ctrl+O (“write out”, сохранить), потом Enter
Ctrl+X (выход)

9. Активируем сайт
```bash
sudo a2ensite glpi.conf
sudo a2enmod rewrite
sudo systemctl reload apache2
```

10. Диагностика

### Проверка дириктории GLPI
Дириктория должна лежать по пути
```
/var/www/html/glpi
```

### Проверка прав на дирикторию
```bash
ls -ld /var/www/html/glpi
```
В идеале владелец — www-data, и права drwxr-xr-x

Если нет, то выполнить
```bash
sudo chown -R www-data:www-data /var/www/html/glpi
sudo chmod -R 755 /var/www/html/glpi
```

### Проверка Apache 

Проверка содержимого glpi.conf
```bash
cat /etc/apache2/sites-available/glpi.conf
```

Проверка слушает ли Apache порт 80
```bash
sudo netstat -tlnp | grep :80
```

Проверка журнала ошибок
```bash
sudo tail -n 40 /var/log/apache2/error.log
```

Перезапуск Apache

```bash
sudo systemctl status apache2
sudo systemctl restart apache2
```

Для проверки доступности с другого устройства в той же сети выполняем:
```bash
curl -I http://10.1.0.19
```

Терминал возвращает:
```bash
curl: (28) Failed to connect to 10.1.0.19 port 80 after 21027 ms: Could not connect to server
```

В данном случае 80 порт не отвечает, проверяем Firewall
```bash
sudo ufw status
```

Терминал возвращает
```bash
Status: active

  

To                         Action      From

--                         ------      ----

22/tcp                     ALLOW       Anywhere

22/tcp (v6)                ALLOW       Anywhere (v6)
```

На сервере политика UFW (Uncomplicated Firewall) — по умолчанию всё закрыто, кроме явно разрешённых портов.
Разрешен только SSH (22), а HTTP (80) был закрыт.

Команда для открытия 80 порта:
```bash
sudo ufw allow 80/tcp
sudo ufw reload
```

Проверяем статус:
```bash
sudo ufw status verbose
```

verbose позволяет "копать глубже"
- Показывает дополнительную информацию:
- Политики по умолчанию (default deny/allow)
- Направления (in/out)
- Интерфейсы
- IPv6/IPv4 правила

Переходим по адресу 10.1.0.19 и попадаем на приветственную страницу Apache
![[telegram-cloud-photo-size-4-5868696266362439872-y.jpg]]

Переходим по адресу 10.1.0.19/glpi и видим, что GLPI доступен
![[telegram-cloud-photo-size-4-5868696266362439895-y.jpg]]

После установки GLPI требует удалить установочный каталог для безопасности:
```bash
sudo rm -rf /var/www/html/glpi/install
```

GLPI стал недоступен

Проверяем лог файл Apache
```bash
sudo tail -n 40 /var/log/apache2/error.log
```

Видим ошибку
```bash
PHP Fatal error:  Uncaught TypeError: Symfony\Component\Cache\Adapter\AbstractAdapter::setLogger(): Argument #1 ($logger) must be of type Psr\Log\LoggerInterface, null given ...
```

GLPI пытается передать несуществующий (null) логгер в кэш-менеджер Symfony.

Это ошибка программной логики, часто связана с одной из причин:
- Недоустановленные зависимости
- Не все модули PHP установлены
- Кэш повреждён
- Ошибка в самой версии GLPI/PHP

Очистка кэша и сессий + правильные права и перезапуск Apache — помогли сбросить ошибочные состояния, и GLPI снова запустился:
```bash
sudo rm -rf /var/www/html/glpi/files/_cache/*
sudo rm -rf /var/www/html/glpi/files/_sessions/*
```

```bash
sudo systemctl restart apache2
```

Финальная проверка логов
```bash
sudo tail -n 40 /var/log/apache2/error.log
```

11. Настройка GLPI в вебе через клиент
Чек-лист GLPI показывает каких параметров по безопасности нехватает
![[telegram-cloud-photo-size-4-5868696266362439904-y.jpg]]

Это не критично, так как установка тестовая, но я настрою конфигурацию безопасности для сессий
```bash
sudo nano /etc/php/8.2/apache2/php.ini
```

Ctrl+W, search “session.cookie_httponly”
```bash
session.cookie_httponly = 
```

Дописать "on", иногда "off" изменить на "on"
```bash
session.cookie_httponly = on
```

перезапуск Apache:
```bash
sudo systemctl restart apache2
```

Обновляем чек-лист и видим изменение
![[telegram-cloud-photo-size-4-5868696266362439909-x.jpg]]

### Подключение БД
База находится на этом же сервере, поэтому вводим localhost или 127.0.0.1 и параметры, которые были заданы выше при настройке БД
![[telegram-cloud-photo-size-4-5868696266362439979-y.jpg]]

Соединяем GLPI с обнаруженной базой
![[telegram-cloud-photo-size-4-5868696266362439981-y.jpg]]
![[telegram-cloud-photo-size-4-5868696266362439982-x.jpg]]

Отказываемся от сбора данных и продолжаем настройку до конца
![[telegram-cloud-photo-size-4-5868696266362439983-x.jpg]]

### Заходим в GLPI под администратором
log / pass: glpi / glpi

Создаем тестовую заявку
![[telegram-cloud-photo-size-4-5868696266362439985-y 3.jpg]]

Версия Установленного GLPI:
10.0.15
![[telegram-cloud-photo-size-4-5868696266362439986-x.jpg]]

Тестовая заявка осталась
![[Pasted image 20250521183155.png]]