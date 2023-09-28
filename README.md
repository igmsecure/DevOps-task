## DevOps-task

#### 1. Реализовать _Firewall_ на `iptables`, в котором будет разделение на цепочки(`chain`) по указанным критериям: [WAFScript](https://github.com/igmsecure/DevOps-task/tree/main/WAFScript)

- _цепочка для адресов, которым разрешено все (все порты)_
- _цепочка для адресов серверов баз данных и контейнеров с приложением, которым разрешено все_
- _цепочка, в которую будут заноситься адреса пользователей, которым нужен доступ по требованию. Им также разрешено все_
- _цепочка, в которую будут заноситься адреса пользователей с временным доступом, им разрешены только определенные порты_
- _цепочка, в которую заносятся порты, смотрящие в мир_

Остальной траффик блокируем и все что блокируем - логируем. Для каждой цепочки организовать свой файл лога. 
В выводе `iptables -L` каждый добавленный адрес должен быть подписан именем.

Ход выполнения: <a href="https://github.com/igmsecure/DevOps-task/tree/main/WAFScript" target="_blank">[WAFScript]</a> 

---

#### 2. Написать скрипт `backup’a`, который: [Backup[Script]](https://github.com/igmsecure/DevOps-task/tree/main/Backup[Script])

1. _Соединяется с другим сервером и копирует данные. Копирование происходит в зашифрованном, сжатом виде_
2. _Есть возможность изменять некоторые параметры при запуске скрипта:_
- _Директория для хранения backup’ов_
- _Пользователь_
- _Сервер, с которым происходит соединение (указывается `IP`)_
- _Есть возможность запуска скрипта в debug режиме_
- _Изменение директорий, которые копируются с удаленного сервера_
- _Возможность выполнения `full` и `incremental backup`_
- _Для ознакомления с имеющимися настройками, использовать ключ `-h` при запуске_
3. _Для ротации устаревших версий используется logrotate._

Логика работы: для `full backup` создается 2 папки (аналогично и для `incremental`):
- _`Full (Inc)` — сохраняется последний backup_
- _`FullOld (IncOld)` — последние backup, именно эти файлы и ротируются_

Ход выполнения: <a href="https://github.com/igmsecure/DevOps-task/tree/main/Backup[Script]" target="_blank">Backup[Script]</a> 

