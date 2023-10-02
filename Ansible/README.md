#### 3. Сформировать роли `Ansible` согласно следующим требованиям: 

1.	_Установка `nginx`_ 
С помощью темплейтов формируется конфиг `nginx` для конкретного домена.
В темплейт передаются переменные с указанием `доменных имен`, `server_name`, `ssl keys`, `enable/disable https`, `generate ssl certs`, `phpsocket`. Так же роль `nginx` должна создавать соотвествующую директорию в `/var/www`

2.	_Установка `php-fpm`_ 
С помощью темплейтов создается конфиг файл php сокета для веб сервера. В темплейт передаются переменные на, основе которых он формируется. Переменные для логов, количество воркеров и тп.

_После применения двух ролей по развернутому домену должен открыться `phpinfo()`;_
