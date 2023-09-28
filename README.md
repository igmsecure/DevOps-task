## DevOps-task

#### 1. Реализовать _Firewall_ на `iptables`, в котором будет разделение на цепочки(`chain`) по указанным критериям:[WAFScript](https://github.com/igmsecure/DevOps-task/tree/main/WAFScript)

- _цепочка для адресов, которым разрешено все (все порты)_
- _цепочка для адресов серверов баз данных и контейнеров с приложением, которым разрешено все_
- _цепочка, в которую будут заноситься адреса пользователей, которым нужен доступ по требованию. Им также разрешено все_
- _цепочка, в которую будут заноситься адреса пользователей с временным доступом, им разрешены только определенные порты_
- _цепочка, в которую заносятся порты, смотрящие в мир_

Остальной траффик блокируем и все что блокируем - логируем. Для каждой цепочки организовать свой файл лога. 
В выводе `iptables -L` каждый добавленный адрес должен быть подписан именем.

<h4 align="center">
  Ход выполнения: <a href="https://github.com/igmsecure/DevOps-task/tree/main/WAFScript" target="_blank">[WAFScript]</a> 
</h4>

`bash`
`#!/bin/bash`

1.1 Создание цепочки для адресов, которым разрешено все (все порты):

- `sudo iptables -N ALLOW_ALL` — создает новую пользовательскую цепочку с именем «ALLOW_AL»L.
- `sudo iptables -A ALLOW_ALL -j ACCEPT` — добавляет правило в цепочку «ALLOW_ALL», которое разрешает все пакеты («-j ACCEPT»).


1.2 Создание цепочки для адресов серверов баз данных и контейнеров с приложением, которым разрешено все:

- `sudo iptables -N DB_APP_SERVERS — создает новую пользовательскую цепочку с именем «DB_APP_SERVERS».
- sudo iptables -A DB_APP_SERVERS -j ACCEPT` — добавляет правило в цепочку «DB_APP_SERVERS», которое разрешает все пакеты (-j ACCEPT).


1.3 Создание цепочки, в которую будут заноситься адреса пользователей, которым нужен доступ по требованию. Им также разрешено все:

- `sudo iptables -N ON_DEMAND_ACCESS` — создает новую пользовательскую цепочку с именем «ON_DEMAND_ACCESS».
- `sudo iptables -A ON_DEMAND_ACCESS -j ACCEPT` — добавляет правило в цепочку «ON_DEMAND_ACCESS», которое

1.4 Создание цепочки, в которую будут заноситься адреса пользователей с временным доступом, им разрешены только определенные порты:

- `sudo iptables -N TEMP_ACCESS` — создает новую пользовательскую цепочку с именем «TEMP_ACCESS».
- `sudo iptables -A TEMP_ACCESS -p tcp --dport <порт> -j ACCEPT` — добавляет правило в цепочку «TEMP_ACCESS», которое разрешает TCP пакеты на указанном порту.
- `sudo iptables -A TEMP_ACCESS -p udp --dport <порт> -j ACCEPT` — добавляет правило в цепочку «TEMP_ACCESS», которое разрешает UDP пакеты на указанном порту.


1.5 Создание цепочки, в которую заносятся порты, смотрящие в мир:

- `sudo iptables -N PUBLIC_PORTS` — создает новую пользовательскую цепочку с именем «PUBLIC_PORTS».
- `sudo iptables -A PUBLIC_PORTS -j ACCEPT` — добавляет правило в цепочку «PUBLIC_PORTS», которое разрешает все пакеты («-j ACCEPT»).


Блокирование остального трафика и логирование:

- `sudo touch /var/log/block_traffic.log` — создание своего файла лога
- `sudo iptables -P INPUT DROP` — устанавливает политику входящего трафика в DROP, что блокирует все пакеты по умолчанию.
- `sudo iptables -A INPUT -j LOG --log-prefix "BLOCKED TRAFFIC: " --log-file /var/log/block_traffic.log` — добавляет правило в цепочку «INPUT», которое логирует все блокируемые пакеты с префиксом "BLOCKED TRAFFIC: ".


Для каждой цепочки организовать свой файл лога:

- `sudo iptables -A ALLOW_ALL -j LOG --log-prefix "ALLOW_ALL: " --log-level 4 --log-file /var/log/allow_all.log` — добавляет правило в цепочку ALLOW_ALL, которое логирует все пакеты с префиксом "ALLOW_ALL: " и записывает их в файл /var/log/allow_all.log.


- `sudo iptables -A DB_APP_SERVERS -j LOG --log-prefix "DB_APP_SERVERS: " --log-level 4 --log-file /var/log/db_app_servers.log` — добавляет правило в цепочку DB_APP_SERVERS, которое логирует все пакеты с префиксом "DB_APP_SERVERS: " и записывает их в файл /var/log/db_app_servers.log.


- `sudo iptables -A ON_DEMAND_ACCESS -j LOG --log-prefix "ON_DEMAND_ACCESS: " --log-level 4 --log-file /var/log/on_demand_access.log` — добавляет правило в цепочку ON_DEMAND_ACCESS, которое логирует все пакеты с префиксом "ON_DEMAND_ACCESS: " и записывает их в файл /var/log/on_demand_access.log.


- `sudo iptables -A TEMP_ACCESS -j LOG --log-prefix "TEMP_ACCESS: " --log-level 4 --log-file /var/log/temp_access.log` — добавляет правило в цепочку TEMP_ACCESS, которое логирует все пакеты с префиксом "TEMP_ACCESS: " и записывает их в файл /var/log/temp_access.log.


- `sudo iptables -A PUBLIC_PORTS -j LOG --log-prefix "PUBLIC_PORTS: " --log-level 4 --log-file /var/log/public_ports.log` — добавляет правило в цепочку PUBLIC_PORTS, которое логирует все пакеты с префиксом "PUBLIC_PORTS: " и записывает их в файл /var/log/public_ports.log.


Вывод команды `iptables -L` должен показывать каждый добавленный адрес с подписью именем.

Применим все правила и сохраним их, чтобы они применялись после перезагрузки системы:

`sudo iptables-save > /etc/iptables/WAFScipt.sh`

Это команда сохранит правила iptables в файл /etc/iptables/WAFScipt.sh.
</hr>


