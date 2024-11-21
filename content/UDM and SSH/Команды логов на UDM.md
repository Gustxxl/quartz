
| Команда Cisco/EdgeOS/VyOS/Лучшее описание                             | Команда SSH UDM/UDM-P                       |
| :-------------------------------------------------------------------- | :------------------------------------------ |
| показать версию                                                       | `info`                                      |
| показать информацию о системе и установленном ПО                      | `ubnt-device-info summary`                  |
| показать температуру процессора                                       | `ubnt-systool cputemp`                      |
| показать скорость вентилятора                                         | `ubnt-fan-speed`                            |
| показать время работы системы                                         | `uptime`                                    |
| показать таблицу маршрутизации IP                                     | `netstat -rt -n`                            |
| показать информацию для технической поддержки (сохранить файл)        | `ubnt-make-support-file <file.tar.gz>`      |
| показать сводку PPP-соединений                                        | `pppstats`                                  |
| показать текущего пользователя                                        | `whoami`                                    |
| показать журнал событий                                               | `cat /var/log/messages`                     |
| показать сводку интерфейсов                                           | `ifstat`                                    |
| показать интерфейсы                                                   | `ifconfig`                                  |
| показать другие устройства Ubiquiti в локальной сети (ubnt-discovery) | `ubnt-tools ubnt-discover`                  |
| показать конфигурацию (беспроводную)                                  | `cat /mnt/data/udapi-config/unif`i          |
| показать DHCP-аренды (для NSname)                                     | `cat /mnt/data/udapi-config/dnsmasq.lease`  |
| захват пакетов                                                        | `tcpdump`                                   |
| завершение работы                                                     | `poweroff`                                  |
| перезагрузка                                                          | `reboot`                                    |
| показать состояние IPsec                                              | `ipsec statusall`                           |
| сброс до заводских настроек                                           | `factory-reset.sh`                          |
| показать сожжённый в системе MAC-адрес                                | `ubnt-tools hwaddr`                         |
| перезапустить веб-интерфейс unifios                                   | `/etc/init.d/S95unifios restart`            |
| воспроизведение звука при загрузке                                    | `aplay /usr/share/sounds/unifi/Welcome.wav` |
| проверить подключение к облаку unifi                                  | `netstat -an`                               |
| включить оболочку                                                     | `os shell`                                  |
| t.d.p                                                                 | `bgnd`                                      |
| t.d.p                                                                 | `infctld`                                   |
| t.d.p                                                                 | `pwcheck`                                   |
| t.d.p                                                                 | `fsync`                                     |
| t.d.p                                                                 | `hwaddr`                                    |
| t.d.p                                                                 | `sysusermerge`                              |

| Описание (Cisco/EdgeOS/VyOS)                     | Команда для UDM/UDM-Pro                                  |
| :----------------------------------------------- | :------------------------------------------------------- |
| показать логи сервера Unifi                      | `cat /mnt/data/unifi-os/unifi/logs/server.log`           |
| показать настройки сервера Unifi                 | `cat /mnt/data/unifi-os/unifi-core/config/settings.yam`l |
| показать HTTP логи сервера Unifi                 | `cat /mnt/data/unifi-os/unifi-core/logs/http.log`        |
| показать HTTP логи сервера Unifi (ошибки)        | `cat /mnt/data/unifi-os/unifi-core/logs/errors.log`      |
| показать логи обнаружения сервера Unifi          | `cat /mnt/data/unifi-os/unifi-core/logs/discovery.log`   |
| показать системные логи Unifi                    | `cat /mnt/data/unifi-os/unifi-core/logs/system.log`      |
| показать последние логи паники консоли           | `cat /sys/fs/pstore/*`                                   |
| показать логи динамического DNS                  | `grep inadyn /var/log/messages`                          |
| показать ARP-таблицу и IPv6 соседей              | `arp -a OR ip neigh`                                     |
| показать туннельные интерфейсы                   | `ip tunnel show`                                         |
| показать информацию о выданных IP-адресах (DHCP) | `cat /mnt/data/udapi-config/dnsmasq.lease`                 |


### Команды общего порядка

Здесь собраны SSH-команды, которые могут понадобиться на устройстве UniFi, в первую очередь.

|Команда|Пример|Описание|
|---|---|---|
|_info_|`info`|Отображение информации об устройстве|
|_set-default_|`set-default`|Сброс к заводским настройкам|
|_set-inform_|`set-inform http://192.168.1.1:8080/inform`|Установка URL контроллера, который должен опознавать оборудование|
|_upgrade_|`upgrade https://<firmware-url>.bin`|Перезапись прошивки|
|_fwupdate_|`fwupdate --url https://<firmware-url>.bin`|Обновление прошивки|
|_reboot_|`reboot`|Перезагрузка устройства|
|_poweroff_|`poweroff`|Выключение устройства|
|_uptime_|`uptime`|Отображение времени непрерывной работы устройства|

### Сетевые команды

Эти SSH-команды помогут вам пофиксить сетевые баги устройств UniFi.

|Команда|Пример|Описание|
|---|---|---|
|_ifconfig_|`ifconfig`|Отображение информации о сетевом интерфейсе|
|_ip address add_|`ip address add 192.168.1.143/24 dev br0`|Присвоение статичного IP-адреса|
|_ip route_|`ip route`|Отображение текущего шлюза|
|_ip router add_|`ip route add default via 192.168.1.1`|Установка шлюза, по умолчанию|
||`echo "nameserver 192.168.1.1" > /etc/resolv.conf`|Установка DNS-сервера|
|_ping_|`ping 192.168.1.101`|Проверка соединения с устройством|
|_arp_|`arp -a`|Отображение таблицы определения адресов|
|_ip neigh_|`ip neigh`|Отображение соседних устройств в сети|

### Команды Unifi OS

Эти команды становятся доступны, когда вы подключаетесь к [Dream Machine Pro](https://ubiquiti.ru/udm-pro.html) или [другому контроллеру с установленной Unifi OS](https://ubiquiti.ru/kontrollery-konsoli-unifi-os.html).

|Команда|Пример|Описание|
|---|---|---|
|_ubnt-systool help_|`ubnt-systool help`|Отображает все команды|
|_ubnt-systool cputemp_|`ubnt-systool cputemp`|Отображает температуру процессора|
|_ubnt-systool cpuload_|`ubnt-systool cpuload`|Отображает загрузку процессора|
|_ubnt-systool portstatus_|`ubnt-systool portstatus`|Отображает статусы портов|
|_ubnt-systool hostname_|`ubnt-systool hostname`|Устанавливает новое имя для хоста|
|_ubnt-systool reboot_|`ubnt-systool reboot`|Перезагрузить устройство|
|_ubnt-systool poweroff_|`ubnt-systool poweroff`|Выключить устройство|
|_ubnt-systool reset2defaults_|`ubnt-systool reset2defaults`|Сброс к заводским настройкам|
|_ubnt-device-info summary_|`ubnt-device-info summary`|Отображение системной информации|
|_ubnt-tools ubnt-discover_|`ubnt-tools ubnt-discover`|Отображение устройств UniFi в сети|
|_cat /mnt/data/udapi-config/dnsmasq.lease_|`cat /mnt/data/udapi-config/dnsmasq.lease`|Отображение арендуемых DHCP адресов|
|_cat /mnt/data/udapi-config/unifi_|`cat /mnt/data/udapi-config/unifi`|Отображение конфигурации|
|_/etc/init.d/S95unifios restart_|`/etc/init.d/S95unifios restart`|Перезапуск web-интерфейса Unifi OS|

### Команды доступа к логам

В UniFi есть множество логов, которые помогут избавиться от ошибок.

| Команда                                                    | Описание                                                              |
| ---------------------------------------------------------- | --------------------------------------------------------------------- |
| `_cat /var/log/messages_`                                  | Вывод лога ошибок                                                     |
| `_tail -f /var/log/messages_`                              | Отображение в реальном времени появляющихся в логе ошибок новых строк |
| `_cat /mnt/data/unifi-os/unifi-core/config/settings.yaml_` | Вывод настроек сервера                                                |
| `_cat /mnt/data/unifi-os/unifi-core/logs/discovery.log_`   | Лог обнаружения оборудования                                          |
| `_cat /mnt/data/unifi-os/unifi-core/logs/system.log_`      | Системный лог                                                         |
| `_cat /mnt/data/unifi-os/unifi/logs/server.log_`           | Лог серверных событий                                                 |
| `_cat /mnt/data/unifi-os/unifi-core/logs/errors.log_`      | Ошибки http                                                           |
