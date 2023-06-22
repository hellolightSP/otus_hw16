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
```
