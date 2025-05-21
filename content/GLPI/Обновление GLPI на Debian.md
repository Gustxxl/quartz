tags: [[GLPI]] [[Десна]] [[IT, Information technology]] [[Linux]] [[Debian]]
___
1. Делаем резервную копию БД
```bash
sudo mysqldump glpi_db > ~/glpi_db_backup_$(date +%F).sql
```
(указываем фактическое имя пользователя и базы, пароль вводим от БД)

 Бэкап всей дириктории GLPI
```bash
sudo cp -r /var/www/html/glpi ~/glpi_backup_$(date +%F)
```

2. Загружаем нужную версию GLPI
```bash
cd /tmp
wget https://github.com/glpi-project/glpi/releases/download/10.0.18/glpi-10.0.18.tgz
tar -xvzf glpi-10.0.18.tgz
```

3. Останавливаем Apache на время обновления
```bash
sudo systemctl stop apache2
```

4. Переименовываем каталог устаревшей версии GLPI
```bash
sudo mv /var/www/html/glpi /var/www/html/glpi_old
```

5. Переносим свежую версию GLPI в /var/www/html/glpi
```bash
sudo mv /tmp/glpi /var/www/html/glpi
```

6. Переносим критические данные в папку:
```bash
sudo cp -r /var/www/html/glpi_old/files /var/www/html/glpi/
sudo cp -r /var/www/html/glpi_old/config /var/www/html/glpi/
sudo cp -r /var/www/html/glpi_old/marketplace /var/www/html/glpi/
```

7. Проверяем права на файлы
```bash
sudo chown -R www-data:www-data /var/www/html/glpi
sudo chmod -R 755 /var/www/html/glpi
```

8. Запускаем Apache
```bash
sudo systemctl start apache2
```

9. Заходим на http://10.1.0.19/glpi
___
![[telegram-cloud-photo-size-4-5868696266362440009-y.jpg]]
GLPI пытается использовать корректную работу с часовыми поясами в MariaDB/MySQL (чтобы даты и время отображались правильно и были одинаковыми для всех функций).

Для этого нужны специальные данные о временных зонах в самой базе (таблицы mysql.time_zone*)

Команда импортирует данные временных зон из системных файлов в базу mysql:
```bash
sudo mysql_tzinfo_to_sql /usr/share/zoneinfo | sudo mysql -u root -p mysql
```

Далее заходим в Mariabd
```bash
sudo mariadb
```

Выдаем права
```sql
GRANT SELECT ON mysql.time_zone_name TO 'glpi_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

Перезапускаем Apache
```bash
sudo systemctl restart apache2
```

Теперь работа со временем корректная
![[telegram-cloud-photo-size-4-5868696266362440011-x.jpg]]
___
![[telegram-cloud-photo-size-4-5868696266362440013-x.jpg]]
GLPI обнаружил, что в дириктории есть лишние, “старые” файлы, и честно предупреждает о возможных проблемах безопасности или багов.
Ошибка вызвана установкой "поверх", при чистой установке такая ошибка не появляется

9. Удаляем установщик
```bash
sudo rm -rf /var/www/html/glpi/install
```

10. Жмем Upgrade
![[Pasted image 20250521182654.png]]
Не отправляем статистику
Нажимаем use GLPI

GLPI обновлен
![[Pasted image 20250521183028.png]]