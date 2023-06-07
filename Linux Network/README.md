## **Part 1. Инструмент ipcalc**

### **1.1. Сети и маски**

- ![Адрес сети ip 192.167.38.54/13](img/1.png)
- Адрес сети: 192.160.0.0

- ![Перевод маски 255.255.255.0 в префиксную и двоичную запись](img/2.png)
- Перевод маски 255.255.255.0: префиксная запись - 24; двоичная запись - 11111111.11111111.11111111.00000000

- ![Перевод маски 15 в обычную и двоичную](img/3.png)
- Перевод маски 15: обычная запись - 255.254.0.0; двоичная запись - 11111111.1111111 0.00000000.00000000

- ![Перевод маски 11111111.11111111.11111111.11110000 в обычную и префиксную](img/4.png)
- Перевод маски 11111111.11111111.11111111.11110000: обычная запись - 255.255.255.0; префиксная запись - 24

- ![Минимальный и максимальный хост в сети 12.167.38.4 при маске 8](img/5.png)
- Минимальный хост в сети 12.167.38.4 при маске 8: 12.0.0.1
- Максимальный хост в сети 12.167.38.4 при маске 8: 12.255.255.254

- ![Минимальный и максимальный хост в сети 12.167.38.4 при маске 11111111.11111111.00000000.00000000](img/6.png)
- Минимальный хост в сети 12.167.38.4 при маске 11111111.11111111.00000000.00000000: 12.167.0.1
- Максимальный хост в сети 12.167.38.4 при маске 11111111.11111111.00000000.00000000: 12.167.255.254

- ![Минимальный и максимальный хост в сети 12.167.38.4 при маске 255.255.254.0](img/7.png)
- Минимальный хост в сети 12.167.38.4 при маске 255.255.254.0: 12.167.38.1
- Максимальный хост в сети 12.167.38.4 при маске 255.255.254.0: 12.167.39.254

- ![Минимальный и максимальный хост в сети 12.167.38.4 при маске 4](img/8.png)
- Минимальный хост в сети 12.167.38.4 при маске 255.255.254.0: 0.0.0.1
- Максимальный хост в сети 12.167.38.4 при маске 255.255.254.0: 15.255.255.254

### **1.2. localhost**

- Для доступа к приложению, работающему на localhost ip адрес устройства должен входить в промежуток 127.0.0.1 — 127.255.255.254
- 194.34.23.100 - не localhost
- 127.0.0.2 - localhost
- 127.1.0.1 - localhost
- 128.0.0.1 - не localhost

### **1.3. Диапазоны и сегменты сетей**

- К частным адресам относятся IP-адреса из следующих подсетей: 10.0.0.0 - 10.255.255.255 с маской 255.0.0.0 или /8; 172.16.0.0 - 172.31.255.255 с маской 255.240.0.0 или /12; 192.168.0.0 - 192.168.255.255 с маской 255.255.0.0 или /16; 100.64.0.0 - 100.127.255.255 с маской подсети 255.192.0.0 или /10.
- 10.0.0.45 - частный
- 134.43.0.2 - публичный
- 192.168.4.2 - частный
- 172.20.250.4 - частный
- 172.0.2.1 - публичный
- 192.172.0.1 - публичный
- 172.68.0.2 - публичный
- 172.16.255.255 - частный
- 10.10.10.10 - частный
- 192.169.168.1 - публичный

- Все адреса входящие в промежуток между HostMin и HostMax подходят:
- ![HostMin и HostMax у сети 10.10.0.0/18](img/9.png)
- 10.0.0.1 - не подходит
- 10.10.0.2 - подходит
- 10.10.10.10 - подходит
- 10.10.100.1 - не подходит
- 10.10.1.255 - подходит

## **Part 2. Статическая маршрутизация между двумя машинами**

- ![Просмотр существующих сетевых интерфейсов на WS1 с помощью команды ip a](img/10.png)
- Просмотр существующих сетевых интерфейсов на WS1 с помощью команды `ip a`

- ![Просмотр существующих сетевых интерфейсов на WS2 с помощью команды ip a](img/11.png)
- Просмотр существующих сетевых интерфейсов на WS2 с помощью команды `ip a`

- ![Описание сетевого интерфейса WS1](img/12.png)
- Описание сетевого интерфейса WS1

- ![Описание сетевого интерфейса WS2](img/13.png)
- Описание сетевого интерфейса WS1

- ![Применение изменений на WS1](img/14.png)
- ![Применение изменений на WS2](img/15.png)
- Применяем изменения, используя команду `sudo netplan apply` на обоих WS

- Добавляем адаптер в настройках виртуальных машин с названием intnet

- ![Новый адаптер на WS1](img/16.png)
- Появился новый адаптер с ip 192.168.100.10 и маской 16 на WS1

- ![Новый адаптер на WS2](img/17.png)
- Появился новый адаптер с ip 172.24.116.8 и маской 12 на WS2

### **2.1. Добавление статического маршрута вручную**

- ![Добавление статического маршрута от WS1 до WS2](img/18.png)
- С помощью команды `sudo ip route add 172.24.116.8 dev enp0s8` добавляем маршрут от WS1 до WS2

- ![Вывод команды ip r для WS1](img/19.png)
- Вывод команды `ip r` для WS1

- ![Добавление статического маршрута от WS2 до WS1](img/20.png)
- С помощью команды `sudo ip route add 192.168.100.10 dev enp0s8` добавляем маршрут от WS2 до WS1

- ![Вывод команды ip r для WS2](img/21.png)
- Вывод команды `ip r` для WS2

- ![Пингуем WS2 с WS1](img/22.png)
- Пинг WS2 с WS1 прошел успешно

- ![Пингуем WS1 с WS2](img/23.png)
- Пинг WS1 с WS2 прошел успешно

### **2.2. Добавление статического маршрута с сохранением**

- ![Добавляем статический маршрут от WS1 до WS2](img/24.png)
- Добавляем статический маршрут от WS1 до WS2

- ![Добавляем статический маршрут от WS2 до WS1](img/25.png)
- Добавляем статический маршрут от WS2 до WS1

- ![Пингуем WS2 с WS1](img/26.png)
- Пинг WS2 с WS1 прошел успешно

- ![Пингуем WS1 с WS2](img/27.png)
- Пинг WS1 с WS2 прошел успешно

## **Part 3. Утилита iperf3**

### **3.1. Скорость соединения**

- 8 Mbps - 1 MB/s (Мегабит/сек в Мегабайт/сек)
- 100 MB/s - 819200 Kbps (Мегабайт/сек в Килобит/сек)
- 1 Gbps - 1024 Mbps (Гигабит/сек в Мегабит/сек)

### **3.2. Утилита iperf3. Измерить скорость между ws1 и ws2**

- ![Запускаем команду iperf3 -s на WS1, которая выступает в роли сервера](img/28.png)
- ![Запускаем команду iperf -c 192.168.100.10 на WS2, которая выступает в роли клиента](img/29.png)
- Сначала запускаем команду `iperf3 -s` на WS1, которая выступает в роли сервера, затем команду `iperf -c 192.168.100.10` на WS2, которая выступает в роли клиента

## **Part 4. Сетевой экран**

### **4.1. Утилита iptables**

- ![Содержимое файла /etc/firewall.sh на WS1](img/30.png)
- ![Содержимое файла /etc/firewall.sh на WS2](img/31.png)
- Содержимое файла /etc/firewall.sh на WS1 и WS2. Разница заключается в порядке команд, утилита iptables выполняет первое прочитанное правило, соответсвенно на WS1 будет выполнятся запрет и пинг не пройдет, а на WS2 наоборот, первым стоит ACCEPT, разрешить прохождение пакета, пинг пройдет

- ![Выдача прав для файла /etc/firewall.sh на WS1](img/32.png)
- Выдача прав для файла /etc/firewall.sh на WS1
- ![Выдача прав для файла /etc/firewall.sh на WS2](img/33.png)
- Выдача прав для файла /etc/firewall.sh на WS2

- ![Запуск файла /etc/firewall.sh на WS1](img/34.png)
- Запуск файла /etc/firewall.sh на WS1
- ![Запуск файла /etc/firewall.sh на WS2](img/35.png)
- Запуск файла /etc/firewall.sh на WS2

- ![Просмотр всех правил во всех цепочках на WS1](img/36.png)
- Просмотр всех правил во всех цепочках на WS1
- ![Просмотр всех правил во всех цепочках на WS2](img/37.png)
- Просмотр всех правил во всех цепочках на WS2

### **4.2. Утилита nmap**

- ![Вывод команды nmap на WS1](img/38.png)
- Вывод команды nmap на WS1

## **Part 5. Статическая маршрутизация сети**

### **5.1. Настройка адресов машин**

- ![Содержимое файла etc/netplan/00-installer-config.yaml для WS11](img/39.png)
- Содержимое файла etc/netplan/00-installer-config.yaml для WS11

- ![Содержимое файла etc/netplan/00-installer-config.yaml для W21](img/40.png)
- Содержимое файла etc/netplan/00-installer-config.yaml для WS21

- ![Содержимое файла etc/netplan/00-installer-config.yaml для WS22](img/41.png)
- Содержимое файла etc/netplan/00-installer-config.yaml для WS22

- ![Содержимое файла etc/netplan/00-installer-config.yaml для R1](img/42.png)
- Содержимое файла etc/netplan/00-installer-config.yaml для R1

- ![Содержимое файла etc/netplan/00-installer-config.yaml для R2](img/43.png)
- Содержимое файла etc/netplan/00-installer-config.yaml для R2

- ![Вывод команды ip -4 a для WS11](img/44.png)
- Вывод команды `ip -4` a для WS11

- ![Вывод команды ip -4 a для WS21](img/45.png)
- Вывод команды `ip -4 a` для WS21

- ![Вывод команды ip -4 a для WS22](img/46.png)
- Вывод команды `ip -4 a` для WS22

- ![Вывод команды ip -4 a для R1](img/47.png)
- Вывод команды `ip -4 a` для R1

- ![Вывод команды ip -4 a для R2](img/48.png)
- Вывод команды `ip -4 a` для R2

- ![Пингуем WS22 с WS21](img/49.png)
- Пингуем WS22 с WS21

- ![Пингуем R1 с WS11](img/50.png)
- Пингуем R1 с WS11

### **5.2. Включение переадресации IP-адресов.**

- ![Включаем переадресацию IP на R1 (до перезагрузки)](img/51.png)
- Включаем переадресацию  IP на R1 с помощью команды `sysctl -w net.ipv4.ip_forward=1` (до перезагрузки)

- ![Включаем переадресацию IP на R2 (до перезагрузки)](img/52.png)
- Включаем переадресацию IP на R2 с помощью команды `sysctl -w net.ipv4.ip_forward=1` (до перезагрузки)

- ![Включаем переадресацию IP на R1 (на постоянной основе)](img/53.png)
- Включаем переадресацию IP на R1 с помощью команды `net.ipv4.ip_forward=1` в файле /etc/sysctl.conf (на постоянной основе)

- ![Включаем переадресацию IP на R2 (на постоянной основе)](img/54.png)
- Включаем переадресацию IP на R2 с помощью команды `sysctl -w net.ipv4.ip_forward=1` в файле /etc/sysctl.conf (на постоянной основе)

### **5.3. Установка маршрута по-умолчанию**

- ![Добавляем gateway4 перед routes с IP первого шлюза на WS11](img/55.png)
- Добавляем gateway4 перед routes с IP первого шлюза на WS11

- ![Добавляем gateway4 перед routes с IP первого шлюза на WS21](img/56.png)
- Добавляем gateway4 перед routes с IP второго шлюза на WS21

- ![Добавляем gateway4 перед routes с IP первого шлюза на WS22](img/57.png)
- Добавляем gateway4 перед routes с IP второго шлюза на WS22

- ![Проверяем добавился ли gateway4 на WS11](img/58.png)
- Проверяем добавился ли gateway4 на WS11

- ![Проверяем добавился ли gateway4 на WS21](img/59.png)
- Проверяем добавился ли gateway4 на WS21

- ![Проверяем добавился ли gateway4 на WS22](img/60.png)
- Проверяем добавился ли gateway4 на WS22

- ![Пингуем R2 с WS11](img/61.png)
- Пингуем R2 с WS11

- ![Пинг доходит до R2](img/62.png)
- Пинг доходит до R2

### **5.4. Добавление статических маршрутов**

- ![Содержимое файла etc/netplan/00-installer-config.yaml для R1](img/63.png)
- Содержимое файла etc/netplan/00-installer-config.yaml для R1

- ![Содержимое файла etc/netplan/00-installer-config.yaml для R2](img/64.png)
- Содержимое файла etc/netplan/00-installer-config.yaml для R2

- ![Вывод команды ip r для R1](img/65.png)
- Вывод команды `ip r` для R1


- ![Вывод команды ip r для R2](img/66.png)
- Вывод команды `ip r` для R2

- ![Запуск команд ip r list 10.10.0.0/18 и ip r list 0.0.0.0/0 для WS11](img/67.png)
- Запуск команд `ip r list 10.10.0.0/18` и `ip r list 0.0.0.0/0` для WS11
- Маршрут был выбран отличный, поскольку процесс оценки маршрута в каждом маршрутизаторе использует метод совпадения самого длинного префикса для получения наиболее точного маршрута. Сеть с самой длинной маской подсети или префиксом сети, которая соответсвует целевому ip-адресу, является сетевым шлюзом следующего перехода. Процесс повторяется до тех пор, пока пакет не будет доставлен на хост назначения. Если вкратце, при наличии двух и более маршрутов выбирается маршрут с самой длинной маской т.к. он более точный

### **5.5. Построение списка маршрутизаторов**

- ![Запуск команды traceroute 10.20.0.10 на WS11](img/68.png)
- Запуск команды `traceroute 10.20.0.10` на WS11

- ![Вывод команды tcpdump -tnv -i enp0s8 на R1](img/69.png)
- Вывод команды tcpdump -tnv -i enp0s8 на R1
- Каждый пакет проходит на своем пути определенное количество узлов, пока достигнет своей цели. Причем, каждый пакет имеет свое время жизни. Это количество узлов, которые может пройти пакет перед тем, как он будет уничтожен. Этот параметр записывается в заголовке TTL, каждый маршрутизатор, через который будет проходить пакет уменьшает его на единицу. При TTL=0 пакет уничтожается, а отправителю отсылается сообщение Time Exceeded.Команда traceroute linux использует UDP пакеты. Она отправляет пакет с TTL=1 и смотрит адрес ответившего узла, дальше TTL=2, TTL=3 и так пока не достигнет цели. Каждый раз отправляется по три пакета и для каждого из них измеряется время прохождения. Пакет отправляется на случайный порт, который, скорее всего, не занят. Когда утилита traceroute получает сообщение от целевого узла о том, что порт недоступен трассировка считается завершенной

### **5.6. Использование протокола ICMP при маршрутизации**

- ![Пингуем несуществующий IP на WS11](img/70.png)
- Пингуем несуществующий IP на WS11

- ![Запускаем на R1 перехват сетевого трафика](img/71.png)
- Запускаем на R1 перехват сетевого трафика 

## **Part 6. Динамическая настройка IP с помощью DHCP**

- Сначала используем команду `sudo apt install isc-dhcp-serverz`, после этого переходим в файл /etc/dhcp/dhcpd.conf и прописываем там настройки
- ![Содержимое файла /etc/dhcp/dhcpd.conf на R2](img/72.png)
- Содержимое файла /etc/dhcp/dhcpd.conf на R2

- ![Содержимое файла /etc/resolv.conf на R2](img/73.png)
- Содержимое файла /etc/resolv.conf на R2

- ![Перезагружаем службу DHCP командой systemctl restart isc-dhcp-server](img/74.png)
- Перезагружаем службу DHCP командой `systemctl restart isc-dhcp-server`

- ![Содержимое файла /etc/netplan/00-installer-config.yaml на WS21](img/75.png)
- Ставим true напротив dhcp, статические настройки комментируем

- ![Вывод команды ip a на WS21](img/76.png)
- Вывод команды ip a на WS21. Присвоенный WS21 ip адрес входит в тот диапазон dhcp, который мы указали в /etc/dhcp/dhcpd.conf

- ![Пингуем WS22 с WS21](img/77.png)
- Пингуем WS22 с WS21

- ![Указываем mac адрес для WS11](img/78.png)
- Указываем mac адрес для WS11

- ![Указываем mac адрес для WS11](img/79.png)
- Указываем mac адрес для WS11 в настройках виртуальной машины

- ![Содержимое файла /etc/dhcp/dhcpd.conf на R1](img/80.png)
- Содержимое файла /etc/dhcp/dhcpd.conf на R1

- ![Содержимое файла /etc/resolv.conf на R1](img/81.png)
- Содержимое файла /etc/resolv.conf на R1

- ![Пингуем R1 с WS11](img/82.png)
- Пингуем R1 с WS11
- Тесты на видимость в локальной сети работают, но отсутствует доступ в интернет. Если переписать приоритет дефолтных шлюзов, можно сменить адаптер на NAT, но тогда локальная сеть перестанет работать. В целом, DNS сервер в файле resolv.conf не имеет смысла, поскольку файл переписывается каждый раз когда происходит рестарт DHCP.

- ![Вывод команды hostname -I на WS21](img/83.png)
- Вывод команды hostname -I на WS21

- ![Запрос на выдачу ip-адреса у DHCP сервера](img/84.png)
- Запрос на выдачу ip-адреса у DHCP сервера
- `range 10.20.0.2 10.20.0.50;` - диапазон доступных IP адресов
- `option routers 10.20.0.1;` - адрес шлюза маршрутизатора
- `option domain-name-servers 10.20.0.1;` - IP адресс DNS-сервера

### **Part 7. NAT**

- Сначала ставим apach при помощи команды `sudo apt install apache2`

- ![Содержимое файла /etc/apache2/ports.conf на WS22](img/85.png)
- Изменяем строку `Listen 80` на `Listen 0.0.0.0:80` на WS22, тем самым делаем сервер общедоступным

- ![Содержимое файла /etc/apache2/ports.conf на R1](img/86.png)
- Изменяем строку `Listen 80` на `Listen 0.0.0.0:80` на R1, тем самым делаем сервер общедоступным

- ![Запускаем веб-сервер на WS22](img/87.png)
- Запускаем веб-сервер на WS22 командой `service apache2 start`

- ![Запускаем веб-сервер на R1](img/88.png)
- Запускаем веб-сервер на R1 командой `service apache2 start`

- ![Содержимое файла /etc/firewall.sh на R2](img/89.png)
- Добавляем правила в фаервол на R2 в соответсвии с заданием

- ![Содержимое файла /etc/firewall.sh на R2](img/90.png)
- Даем скрипту права и запускаем

- ![Пингуем R1 с WS22](img/91.png)
- Пингуем R1 с WS22

- ![Содержимое файла /etc/firewall.sh на R2](img/92.png)
- Добавляем еще одно правило для пропуска icmp

- ![Пингуем R1 с WS22](img/93.png)
- Пингуем R1 с WS22

- ![Содержимое файла /etc/firewall.sh на R2](img/94.png)
- Включаем SNAT, DNAT, добавляем правило, которое разрешает TCP

- ![Коннектимся к R1 через telnet на WS22](img/95.png)
- Коннектимся к R1 через telnet на WS22 (проверка SNAT)

- ![Коннектимся к WS22 через telnet на R1](img/96.png)
- Коннектимся к WS22 через telnet на R1 (проверка DNAT)

## **Part 8. Дополнительно. Знакомство с SSH Tunnels**

- ![Меняем в /etc/apache2/ports.conf порт на local](img/97.png)
- Меняем в /etc/apache2/ports.conf порт на local

- ![Запускаем apache на WS22 с новыми настройками](img/98.png)
- Запускаем apache на WS22 с новыми настройками

- ![Проверка работы сервера](img/99.png)
- Проверка работы сервера

- ![Подключаемся к WS22 с WS21](img/100.png)
- Подключаемся к WS22 с WS21

- ![Подключаемся к WS22 с WS11](img/101.png)
- Подключаемся к WS22 с WS11

- ![Проверка подключения](img/102.png)
- Проверка подключения