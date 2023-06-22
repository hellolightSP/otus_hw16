**Домашние задание**

**Что нужно сделать**

- с помощью Vagrant поднимаем 2 машины web и log
- на web поднимаем nginx
- на log настраиваем центральный лог сервер на любой системе на выбор, выбрал rsyslog
- настраиваем аудит, следящий за изменением конфигов нжинкса
- Все критичные логи с web должны собираться и локально и удаленно.
- Все логи с nginx должны уходить на удаленный сервер (локально только критичные).
- Логи аудита должны также уходить на удаленную систему.
- Формат сдачи ДЗ - vagrant + ansible

**Выполнение**

- Следуя инструциям в методичке https://docs.google.com/document/d/16UBAMu4LYqvRv6PmCeHcmOampMrIZavH/edit создал [Vagrantfile](https://github.com/hellolightSP/otus_hw16/blob/main/Vagrantfile)
- Написал автоматизацию на [ansible](https://github.com/hellolightSP/otus_hw16/tree/main/ansible/syslog/ansible)
- [Лог развертывания](https://github.com/hellolightSP/otus_hw16/blob/main/otus_hw16_syslog) 
- После раскатки Vagrant заходим на сервер log и проверяем что на него пишутся error и access логи nginx и логи audit'a, приходящие с сервера web:

```
[root@log vagrant]# cat /var/log/rsyslog/web/nginx_access.log 
Jun 22 17:34:30 web nginx_access: 192.168.56.1 - - [22/Jun/2023:17:34:30 +0300] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
Jun 22 17:34:31 web nginx_access: 192.168.56.1 - - [22/Jun/2023:17:34:31 +0300] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
Jun 22 17:34:31 web nginx_access: message repeated 3 times: [ 192.168.56.1 - - [22/Jun/2023:17:34:31 +0300] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"]
Jun 22 17:34:32 web nginx_access: 192.168.56.1 - - [22/Jun/2023:17:34:32 +0300] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
Jun 22 17:34:32 web nginx_access: message repeated 4 times: [ 192.168.56.1 - - [22/Jun/2023:17:34:32 +0300] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"]
Jun 22 17:34:59 web nginx_access: 192.168.56.1 - - [22/Jun/2023:17:34:59 +0300] "GET /t HTTP/1.1" 404 3650 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
Jun 22 17:35:00 web nginx_access: 192.168.56.1 - - [22/Jun/2023:17:35:00 +0300] "GET /t HTTP/1.1" 404 3650 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
Jun 22 17:35:01 web nginx_access: 192.168.56.1 - - [22/Jun/2023:17:35:01 +0300] "GET /t HTTP/1.1" 404 3650 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
Jun 22 17:35:01 web nginx_access: 192.168.56.1 - - [22/Jun/2023:17:35:01 +0300] "GET /t HTTP/1.1" 404 3650 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
Jun 22 17:35:01 web nginx_access: 192.168.56.1 - - [22/Jun/2023:17:35:01 +0300] "GET /t HTTP/1.1" 404 3650 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
Jun 22 17:35:01 web nginx_access: 192.168.56.1 - - [22/Jun/2023:17:35:01 +0300] "GET /t HTTP/1.1" 404 3650 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
Jun 22 17:35:01 web nginx_access: 192.168.56.1 - - [22/Jun/2023:17:35:01 +0300] "GET /t HTTP/1.1" 404 3650 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"
Jun 22 17:35:01 web nginx_access: 192.168.56.1 - - [22/Jun/2023:17:35:01 +0300] "GET /t HTTP/1.1" 404 3650 "-" "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/113.0.0.0 Safari/537.36"

[root@log vagrant]# cat /var/log/rsyslog/web/nginx_error.log 
Jun 22 17:34:59 web nginx_error: 2023/06/22 17:34:59 [error] 4008#4008: *1 open() "/usr/share/nginx/html/t" failed (2: No such file or directory), client: 192.168.56.1, server: _, request: "GET /t HTTP/1.1", host: "192.168.56.10"
Jun 22 17:35:00 web nginx_error: 2023/06/22 17:35:00 [error] 4008#4008: *1 open() "/usr/share/nginx/html/t" failed (2: No such file or directory), client: 192.168.56.1, server: _, request: "GET /t HTTP/1.1", host: "192.168.56.10"
Jun 22 17:35:01 web nginx_error: 2023/06/22 17:35:01 [error] 4008#4008: *1 open() "/usr/share/nginx/html/t" failed (2: No such file or directory), client: 192.168.56.1, server: _, request: "GET /t HTTP/1.1", host: "192.168.56.10"
Jun 22 17:35:01 web nginx_error: 2023/06/22 17:35:01 [error] 4008#4008: *1 open() "/usr/share/nginx/html/t" failed (2: No such file or directory), client: 192.168.56.1, server: _, request: "GET /t HTTP/1.1", host: "192.168.56.10"
Jun 22 17:35:01 web nginx_error: 2023/06/22 17:35:01 [error] 4008#4008: *1 open() "/usr/share/nginx/html/t" failed (2: No such file or directory), client: 192.168.56.1, server: _, request: "GET /t HTTP/1.1", host: "192.168.56.10"
Jun 22 17:35:01 web nginx_error: 2023/06/22 17:35:01 [error] 4008#4008: *1 open() "/usr/share/nginx/html/t" failed (2: No such file or directory), client: 192.168.56.1, server: _, request: "GET /t HTTP/1.1", host: "192.168.56.10"
Jun 22 17:35:01 web nginx_error: 2023/06/22 17:35:01 [error] 4008#4008: *1 open() "/usr/share/nginx/html/t" failed (2: No such file or directory), client: 192.168.56.1, server: _, request: "GET /t HTTP/1.1", host: "192.168.56.10"

[root@log vagrant]# cat /var/log/audit/audit.log | grep web
node=web type=DAEMON_START msg=audit(1687445259.365:9630): op=start ver=2.8.5 format=raw kernel=3.10.0-1127.el7.x86_64 auid=4294967295 pid=4022 uid=0 ses=4294967295 subj=system_u:system_r:auditd_t:s0 res=success
node=web type=CONFIG_CHANGE msg=audit(1687445259.519:1253): audit_backlog_limit=8192 old=8192 auid=4294967295 ses=4294967295 subj=system_u:system_r:unconfined_service_t:s0 res=1
node=web type=CONFIG_CHANGE msg=audit(1687445259.520:1254): audit_failure=1 old=1 auid=4294967295 ses=4294967295 subj=system_u:system_r:unconfined_service_t:s0 res=1
node=web type=CONFIG_CHANGE msg=audit(1687445259.520:1255): auid=4294967295 ses=4294967295 subj=system_u:system_r:unconfined_service_t:s0 op=add_rule key="nginx_conf" list=4 res=1
node=web type=CONFIG_CHANGE msg=audit(1687445259.524:1256): auid=4294967295 ses=4294967295 subj=system_u:system_r:unconfined_service_t:s0 op=add_rule key="nginx_conf" list=4 res=1
node=web type=SERVICE_START msg=audit(1687445259.525:1257): pid=1 uid=0 auid=4294967295 ses=4294967295 subj=system_u:system_r:init_t:s0 msg='unit=auditd comm="systemd" exe="/usr/lib/systemd/systemd" hostname=? addr=? terminal=? res=success'

```
