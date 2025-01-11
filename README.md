# Домашнее задание к занятию "Cистема мониторинга Prometheus" - Еноктаев Олег



### Задание 1

Установите Prometheus

Процесс выполнения
1. Выполняя задание, сверяйтесь с процессом, отражённым в записи лекции
2. Создайте пользователя prometheus
3. Скачайте prometheus и в соответствии с лекцией разместите файлы в целевые директории
4. Создайте сервис как показано на уроке
5. Проверьте что prometheus запускается, останавливается, перезапускается и отображает статус с помощью systemctl
Требования к результату
 Прикрепите к файлу README.md скриншот systemctl status prometheus, где будет написано: prometheus.service — Prometheus Service Netology Lesson 9.4 — [Ваши ФИО]

1.2 Создание пользователя prometheus:
```
useradd  --no-create-home --shell /bin/false prometheus
```
1.3 Скачаем prometheus:
```
wget https://github.com/incid3nt/prometheus/blob/main/tar/prometheus-2.40.2.linux-amd64.tar.gz
```
распакуем архив:
```
tar xvfz prometheus-2.40.2.linux-amd64.tar.gz
```
посмотрим содержимое директории:
```
root@prometheus:~/prometheus-2.40.2.linux-amd64# ls
console_libraries  LICENSE  prometheus      promtool
consoles           NOTICE   prometheus.yml
```
скопируем файлы в нужные дирректории:
```
cp ./prometheus promtool /usr/local/bin
cp -R ./console_libraries/ /etc/prometheus/
cp -R ./consoles/ /etc/prometheus/
cp ./prometheus.yml /etc/prometheus/
cp ./prometheus /usr/local/bin
cp ./promtool /usr/local/bin
```
выдаем нужные права:
```
chown -R prometheus:prometheus /etc/prometheus/ /var/lib/prometheus/
chown prometheus:prometheus /usr/local/bin/prometheus
chown prometheus:prometheus /usr/local/bin/promtool
```
Пробуем запустить:
```
/usr/local/bin/prometheus \
  --config.file /etc/prometheus/prometheus.yml \
  --storage.tsdb.path /var/lib/prometheus/ \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries
  ```
  Как видим, все успешно запустилось, но нам же не удобно будет каждый раз запускать вручную, создадим сервис:

1.4 Создаем сервис для prometheus
- nano /etc/systemd/system/prometheus.service
```
[Unit]
Description=Prometheus Service Netology Lesson 9.4 - [Еноктаев Олег Владимирович]
After=network.target
[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/usr/local/bin/prometheus \
--config.file /etc/prometheus/prometheus.yml \
--storage.tsdb.path /var/lib/prometheus/ \
--web.console.templates=/etc/prometheus/consoles \
--web.console.libraries=/etc/prometheus/console_libraries
ExecReload=/bin/kill -HUP $MAINPID Restart=on-failure
[Install]
WantedBy=multi-user.target
```
1.5 systemctl status prometheus.service
![systemctl](https://github.com/incid3nt/prometheus/blob/main/img/putty_gG9QB4PZcc.png)




---

### Задание 2

Установите Node Exporter.

1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Скачайте node exporter приведённый в презентации и в соответствии с лекцией разместите файлы в целевые директории
3. Создайте сервис для как показано на уроке
4. Проверьте что node exporter запускается, останавливается, перезапускается и отображает статус с помощью systemctl

Требования к результату
Прикрепите к файлу README.md скриншот systemctl status node-exporter, где будет написано: node-exporter.service — Node Exporter Netology Lesson 9.4 — [Ваши ФИО]

```
wget https://github.com/incid3nt/prometheus/blob/main/tar/node_exporter-1.4.0.linux-amd64.tar.gz
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 2](ссылка на скриншот 2)`


---

### Задание 3

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`

### Задание 4

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`

```bash
root@prometheus:~# wget https://github.com/prometheus/prometheus/releases/downlo                                             ad/v2.40.2/prometheus-2.40.2.linux-amd64.tar.gz
--2025-01-11 13:19:58--  https://github.com/prometheus/prometheus/releases/downl                                             oad/v2.40.2/prometheus-2.40.2.linux-amd64.tar.gz
Распознаётся github.com (github.com)… 140.82.121.4
Подключение к github.com (github.com)|140.82.121.4|:443... соединение установлен                                             о.
HTTP-запрос отправлен. Ожидание ответа… 302 Found
Адрес: https://objects.githubusercontent.com/github-production-release-asset-2e6                                             5be/6838921/2ad88d1f-8b79-4cfa-93a3-f5ccb59c3357?X-Amz-Algorithm=AWS4-HMAC-SHA25                                             6&X-Amz-Credential=releaseassetproduction%2F20250111%2Fus-east-1%2Fs3%2Faws4_req                                             uest&X-Amz-Date=20250111T101959Z&X-Amz-Expires=300&X-Amz-Signature=6a05cfa549f9d                                             b018daf977ab974f348a2027f507eaef25e8e6e8d4a054928f7&X-Amz-SignedHeaders=host&res                                             ponse-content-disposition=attachment%3B%20filename%3Dprometheus-2.40.2.linux-amd                                             64.tar.gz&response-content-type=application%2Foctet-stream [переход]
--2025-01-11 13:19:59--  https://objects.githubusercontent.com/github-production                                             -release-asset-2e65be/6838921/2ad88d1f-8b79-4cfa-93a3-f5ccb59c3357?X-Amz-Algorit                                             hm=AWS4-HMAC-SHA256&X-Amz-Credential=releaseassetproduction%2F20250111%2Fus-east                                             -1%2Fs3%2Faws4_request&X-Amz-Date=20250111T101959Z&X-Amz-Expires=300&X-Amz-Signa                                             ture=6a05cfa549f9db018daf977ab974f348a2027f507eaef25e8e6e8d4a054928f7&X-Amz-Sign                                             edHeaders=host&response-content-disposition=attachment%3B%20filename%3Dprometheu                                             s-2.40.2.linux-amd64.tar.gz&response-content-type=application%2Foctet-stream
Распознаётся objects.githubusercontent.com (objects.githubusercontent.com)… 185.                                             199.108.133, 185.199.109.133, 185.199.110.133, ...
Подключение к objects.githubusercontent.com (objects.githubusercontent.com)|185.                                             199.108.133|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 200 OK
Длина: 87774959 (84M) [application/octet-stream]
Сохранение в: «prometheus-2.40.2.linux-amd64.tar.gz»

prometheus-2.40.2.l 100%[===================>]  83,71M  6,36MB/s    за 32s

2025-01-11 13:20:32 (2,60 MB/s) - «prometheus-2.40.2.linux-amd64.tar.gz» сохранё                                             н [87774959/87774959]

root@prometheus:~# ls
prometheus-2.40.2.linux-amd64.tar.gz
root@prometheus:~# tar xvfz prometheus-2.40.2.linux-amd64.tar.gz
prometheus-2.40.2.linux-amd64/
prometheus-2.40.2.linux-amd64/NOTICE
prometheus-2.40.2.linux-amd64/prometheus
prometheus-2.40.2.linux-amd64/LICENSE
prometheus-2.40.2.linux-amd64/console_libraries/
prometheus-2.40.2.linux-amd64/console_libraries/menu.lib
prometheus-2.40.2.linux-amd64/console_libraries/prom.lib
prometheus-2.40.2.linux-amd64/promtool
prometheus-2.40.2.linux-amd64/prometheus.yml
prometheus-2.40.2.linux-amd64/consoles/
prometheus-2.40.2.linux-amd64/consoles/prometheus-overview.html
prometheus-2.40.2.linux-amd64/consoles/prometheus.html
prometheus-2.40.2.linux-amd64/consoles/node-cpu.html
prometheus-2.40.2.linux-amd64/consoles/node-overview.html
prometheus-2.40.2.linux-amd64/consoles/node-disk.html
prometheus-2.40.2.linux-amd64/consoles/index.html.example
prometheus-2.40.2.linux-amd64/consoles/node.html
root@prometheus:~# ls
prometheus-2.40.2.linux-amd64  prometheus-2.40.2.linux-amd64.tar.gz
root@prometheus:~# rm prometheus-2.40.2.linux-amd64.tar.gz
root@prometheus:~# ls
prometheus-2.40.2.linux-amd64
root@prometheus:~# cd prometheus-2.40.2.linux-amd64/
root@prometheus:~/prometheus-2.40.2.linux-amd64# ls
console_libraries  LICENSE  prometheus      promtool
consoles           NOTICE   prometheus.yml
root@prometheus:~/prometheus-2.40.2.linux-amd64# cp ./prometheus promtool /usr/l                                             ocal/bin
root@prometheus:~/prometheus-2.40.2.linux-amd64# cp -R ./console_libraries/ /etc                                             /prometheus/
root@prometheus:~/prometheus-2.40.2.linux-amd64# cp -R ./consoles/ /etc/promethe                                             us/
root@prometheus:~/prometheus-2.40.2.linux-amd64# cp ./prometheus.yml /etc/promet                                             heus/
root@prometheus:~/prometheus-2.40.2.linux-amd64# ls -l /etc/prometheus/
итого 12
drwxr-xr-x 2 root root 4096 янв 11 13:24 console_libraries
drwxr-xr-x 2 root root 4096 янв 11 13:24 consoles
-rw-r--r-- 1 root root  934 янв 11 13:25 prometheus.yml
root@prometheus:~/prometheus-2.40.2.linux-amd64# chown - R prometheus:prometheus /etc/pro
profile     profile.d/  prometheus/ protocols
root@prometheus:~/prometheus-2.40.2.linux-amd64# chown - R prometheus:prometheus /etc/prometheus/ /var/lib/prometheus/
chown: неверный пользователь: «-»
root@prometheus:~/prometheus-2.40.2.linux-amd64# chown -R prometheus:prometheus /etc/prometheus/ /var/lib/prometheus/
root@prometheus:~/prometheus-2.40.2.linux-amd64# ls -l /etc/prometheus/
итого 12
drwxr-xr-x 2 prometheus prometheus 4096 янв 11 13:24 console_libraries
drwxr-xr-x 2 prometheus prometheus 4096 янв 11 13:24 consoles
-rw-r--r-- 1 prometheus prometheus  934 янв 11 13:25 prometheus.yml
root@prometheus:~/prometheus-2.40.2.linux-amd64# chown prometheus:prometheus /usr/local/bin/prometheus
root@prometheus:~/prometheus-2.40.2.linux-amd64# chown prometheus:prometheus /usr/local/bin/promtool
root@prometheus:~/prometheus-2.40.2.linux-amd64# /usr/local/bin/prometheus --config.file /etc/prometheus/prometheus.yml --storage.tsdb.path /var/lib/prometheus/ --web.console.templates=/etc/prometheus/consoles -- web.console.libraries=/etc/prometheus/console_libraries
Error parsing commandline arguments: unexpected web.console.libraries=/etc/prometheus/console_libraries
prometheus: error: unexpected web.console.libraries=/etc/prometheus/console_libraries
root@prometheus:~/prometheus-2.40.2.linux-amd64# ^C
root@prometheus:~/prometheus-2.40.2.linux-amd64# /usr/local/bin/prometheus \
  --config.file /etc/prometheus/prometheus.yml \
  --storage.tsdb.path /var/lib/prometheus/ \
  --web.console.templates=/etc/prometheus/consoles \
  --web.console.libraries=/etc/prometheus/console_libraries
ts=2025-01-11T10:32:12.847Z caller=main.go:512 level=info msg="No time or size retention was set so using the default time retention" duration=15d
ts=2025-01-11T10:32:12.847Z caller=main.go:556 level=info msg="Starting Prometheus Server" mode=server version="(version=2.40.2, branch=HEAD, revision=a07a94a5abb8a979d8aa87297f77f3979148b2da)"
ts=2025-01-11T10:32:12.847Z caller=main.go:561 level=info build_context="(go=go1.19.3, user=root@1b4b53e3f125, date=20221117-13:40:12)"
ts=2025-01-11T10:32:12.847Z caller=main.go:562 level=info host_details="(Linux 6.1.0-28-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.119-1 (2024-11-22) x86_64 prometheus (none))"
ts=2025-01-11T10:32:12.847Z caller=main.go:563 level=info fd_limits="(soft=1048576, hard=1048576)"
ts=2025-01-11T10:32:12.847Z caller=main.go:564 level=info vm_limits="(soft=unlimited, hard=unlimited)"
ts=2025-01-11T10:32:12.848Z caller=web.go:559 level=info component=web msg="Start listening for connections" address=0.0.0.0:9090
ts=2025-01-11T10:32:12.848Z caller=main.go:993 level=info msg="Starting TSDB ..."
ts=2025-01-11T10:32:12.849Z caller=tls_config.go:232 level=info component=web msg="Listening on" address=[::]:9090
ts=2025-01-11T10:32:12.849Z caller=tls_config.go:235 level=info component=web msg="TLS is disabled." http2=false address=[::]:9090
ts=2025-01-11T10:32:12.852Z caller=head.go:562 level=info component=tsdb msg="Replaying on-disk memory mappable chunks if any"
ts=2025-01-11T10:32:12.852Z caller=head.go:606 level=info component=tsdb msg="On-disk memory mappable chunks replay completed" duration=1.46µs
ts=2025-01-11T10:32:12.852Z caller=head.go:612 level=info component=tsdb msg="Replaying WAL, this may take a while"
ts=2025-01-11T10:32:12.852Z caller=head.go:683 level=info component=tsdb msg="WAL segment loaded" segment=0 maxSegment=0
ts=2025-01-11T10:32:12.852Z caller=head.go:720 level=info component=tsdb msg="WAL replay completed" checkpoint_replay_duration=18.022µs wal_replay_duration=114.511µs wbl_replay_duration=108ns total_replay_duration=154.312µs
ts=2025-01-11T10:32:12.853Z caller=main.go:1014 level=info fs_type=EXT4_SUPER_MAGIC
ts=2025-01-11T10:32:12.853Z caller=main.go:1017 level=info msg="TSDB started"
ts=2025-01-11T10:32:12.853Z caller=main.go:1197 level=info msg="Loading configuration file" filename=/etc/prometheus/prometheus.yml
ts=2025-01-11T10:32:12.853Z caller=main.go:1234 level=info msg="Completed loading of configuration file" filename=/etc/prometheus/prometheus.yml totalDuration=277.079µs db_storage=567ns remote_storage=729ns web_handler=246ns query_engine=768ns scrape=109.98µs scrape_sd=13.787µs notify=21.191µs notify_sd=4.24µs rules=661ns tracing=6.059µs
ts=2025-01-11T10:32:12.853Z caller=main.go:978 level=info msg="Server is ready to receive web requests."
ts=2025-01-11T10:32:12.853Z caller=manager.go:944 level=info component="rule manager" msg="Starting rule manager..."
^Cts=2025-01-11T10:34:48.700Z caller=main.go:828 level=warn msg="Received SIGTERM, exiting gracefully..."
ts=2025-01-11T10:34:48.700Z caller=main.go:852 level=info msg="Stopping scrape discovery manager..."
ts=2025-01-11T10:34:48.700Z caller=main.go:866 level=info msg="Stopping notify discovery manager..."
ts=2025-01-11T10:34:48.700Z caller=manager.go:958 level=info component="rule manager" msg="Stopping rule manager..."
ts=2025-01-11T10:34:48.700Z caller=manager.go:968 level=info component="rule manager" msg="Rule manager stopped"
ts=2025-01-11T10:34:48.700Z caller=main.go:903 level=info msg="Stopping scrape manager..."
ts=2025-01-11T10:34:48.700Z caller=main.go:862 level=info msg="Notify discovery manager stopped"
ts=2025-01-11T10:34:48.700Z caller=main.go:848 level=info msg="Scrape discovery manager stopped"
ts=2025-01-11T10:34:48.701Z caller=main.go:895 level=info msg="Scrape manager stopped"
ts=2025-01-11T10:34:48.762Z caller=notifier.go:608 level=info component=notifier msg="Stopping notification manager..."
ts=2025-01-11T10:34:48.763Z caller=main.go:1123 level=info msg="Notifier manager stopped"
ts=2025-01-11T10:34:48.763Z caller=main.go:1135 level=info msg="See you next time!"
root@prometheus:~/prometheus-2.40.2.linux-amd64# ^C
root@prometheus:~/prometheus-2.40.2.linux-amd64# nano /etc/systemd/system/prometheus.service^C
root@prometheus:~/prometheus-2.40.2.linux-amd64# cd /etc/systemd/system
root@prometheus:/etc/systemd/system# ls
dbus-org.freedesktop.timesync1.service  multi-user.target.wants      sockets.target.wants  sysinit.target.wants
getty.target.wants                      network-online.target.wants  sshd.service          timers.target.wants
root@prometheus:/etc/systemd/system# cd ..
root@prometheus:/etc/systemd# ls
journald.conf  network        pstore.conf  system       timesyncd.conf  user.conf
logind.conf    networkd.conf  sleep.conf   system.conf  user
root@prometheus:/etc/systemd# ^C
root@prometheus:/etc/systemd# nano /etc/systemd/system/prometheus.service
root@prometheus:/etc/systemd# ls -al /var/lib/prometheus
итого 20
drwxr-xr-x  4 prometheus prometheus  4096 янв 11 13:34 .
drwxr-xr-x 27 root       root        4096 янв 11 13:11 ..
drwxr-xr-x  2 root       root        4096 янв 11 13:32 chunks_head
-rw-r--r--  1 root       root       20001 янв 11 13:33 queries.active
drwxr-xr-x  2 root       root        4096 янв 11 13:32 wal
root@prometheus:/etc/systemd# chown -R prometheus:prometheus /var/lib/prometheus
root@prometheus:/etc/systemd# systemctl enable prometheus
Created symlink /etc/systemd/system/multi-user.target.wants/prometheus.service → /etc/systemd/system/prometheus.service.
root@prometheus:/etc/systemd# systemctl status prometheus
○ prometheus.service - Prometheus Service Netology Lesson 9.4
     Loaded: loaded (/etc/systemd/system/prometheus.service; enabled; preset: enabled)
     Active: inactive (dead)
root@prometheus:/etc/systemd# systemctl start prometheus
root@prometheus:/etc/systemd# systemctl status prometheus
● prometheus.service - Prometheus Service Netology Lesson 9.4
     Loaded: loaded (/etc/systemd/system/prometheus.service; enabled; preset: enabled)
     Active: active (running) since Sat 2025-01-11 13:44:02 MSK; 1s ago
   Main PID: 911 (prometheus)
      Tasks: 10 (limit: 4640)
     Memory: 20.7M
        CPU: 47ms
     CGroup: /system.slice/prometheus.service
             └─911 /usr/local/bin/prometheus --config.file /etc/prometheus/prometheus.yml --storage.tsdb.path /var/lib/prome>

янв 11 13:44:02 prometheus prometheus[911]: ts=2025-01-11T10:44:02.072Z caller=head.go:612 level=info component=tsdb msg="Re>
янв 11 13:44:02 prometheus prometheus[911]: ts=2025-01-11T10:44:02.075Z caller=head.go:683 level=info component=tsdb msg="WA>
янв 11 13:44:02 prometheus prometheus[911]: ts=2025-01-11T10:44:02.076Z caller=head.go:683 level=info component=tsdb msg="WA>
янв 11 13:44:02 prometheus prometheus[911]: ts=2025-01-11T10:44:02.076Z caller=head.go:720 level=info component=tsdb msg="WA>
янв 11 13:44:02 prometheus prometheus[911]: ts=2025-01-11T10:44:02.076Z caller=main.go:1014 level=info fs_type=EXT4_SUPER_MA>
янв 11 13:44:02 prometheus prometheus[911]: ts=2025-01-11T10:44:02.076Z caller=main.go:1017 level=info msg="TSDB started"
янв 11 13:44:02 prometheus prometheus[911]: ts=2025-01-11T10:44:02.076Z caller=main.go:1197 level=info msg="Loading configur>
янв 11 13:44:02 prometheus prometheus[911]: ts=2025-01-11T10:44:02.076Z caller=main.go:1234 level=info msg="Completed loadin>
янв 11 13:44:02 prometheus prometheus[911]: ts=2025-01-11T10:44:02.076Z caller=main.go:978 level=info msg="Server is ready t>
янв 11 13:44:02 prometheus prometheus[911]: ts=2025-01-11T10:44:02.077Z caller=manager.go:944 level=info component="rule man>
lines 1-20/20 (END)
root@prometheus:/etc/systemd# ^C
root@prometheus:/etc/systemd# systemctl stop prometheus
root@prometheus:/etc/systemd# systemctl start prometheus
root@prometheus:/etc/systemd# cd
root@prometheus:~# ls
prometheus-2.40.2.linux-amd64
root@prometheus:~# ls -al
итого 40
drwx------  5 root       root 4096 янв 11 13:56 .
drwxr-xr-x 18 root       root 4096 дек  9 23:45 ..
-rw-------  1 root       root   41 янв  4 20:06 .bash_history
-rw-r--r--  1 root       root  571 апр 10  2021 .bashrc
-rw-------  1 root       root   20 янв 11 13:56 .lesshst
drwxr-xr-x  3 root       root 4096 янв  4 20:07 .local
-rw-r--r--  1 root       root  161 июл  9  2019 .profile
drwxr-xr-x  4 prometheus  121 4096 ноя 17  2022 prometheus-2.40.2.linux-amd64
drwx------  2 root       root 4096 дек  9 23:39 .ssh
-rw-r--r--  1 root       root  165 янв 11 13:20 .wget-hsts
root@prometheus:~# wget https://github.com/prometheus/node_exporter/releases/download/v1.4.0/node_exporter-1.4.0.linux-amd64.tar.gz
--2025-01-11 14:15:48--  https://github.com/prometheus/node_exporter/releases/download/v1.4.0/node_exporter-1.4.0.linux-amd64.tar.gz
Распознаётся github.com (github.com)… 140.82.121.3
Подключение к github.com (github.com)|140.82.121.3|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 302 Found
Адрес: https://objects.githubusercontent.com/github-production-release-asset-2e65be/9524057/5fdacb9b-a17a-4b4a-b2f0-f2946771d4ca?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=releaseassetproduction%2F20250111%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250111T111549Z&X-Amz-Expires=300&X-Amz-Signature=58694611c56c0cec153312d9f849fb909ac47762f459939f0201e809f6e1b7cf&X-Amz-SignedHeaders=host&response-content-disposition=attachment%3B%20filename%3Dnode_exporter-1.4.0.linux-amd64.tar.gz&response-content-type=application%2Foctet-stream [переход]
--2025-01-11 14:15:49--  https://objects.githubusercontent.com/github-production-release-asset-2e65be/9524057/5fdacb9b-a17a-4b4a-b2f0-f2946771d4ca?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=releaseassetproduction%2F20250111%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Date=20250111T111549Z&X-Amz-Expires=300&X-Amz-Signature=58694611c56c0cec153312d9f849fb909ac47762f459939f0201e809f6e1b7cf&X-Amz-SignedHeaders=host&response-content-disposition=attachment%3B%20filename%3Dnode_exporter-1.4.0.linux-amd64.tar.gz&response-content-type=application%2Foctet-stream
Распознаётся objects.githubusercontent.com (objects.githubusercontent.com)… 185.199.108.133, 185.199.109.133, 185.199.110.133, ...
Подключение к objects.githubusercontent.com (objects.githubusercontent.com)|185.199.108.133|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 200 OK
Длина: 10111972 (9,6M) [application/octet-stream]
Сохранение в: «node_exporter-1.4.0.linux-amd64.tar.gz»

node_exporter-1.4.0.linux-amd64 100%[====================================================>]   9,64M  3,52MB/s    за 2,7s

2025-01-11 14:15:52 (3,52 MB/s) - «node_exporter-1.4.0.linux-amd64.tar.gz» сохранён [10111972/10111972]

root@prometheus:~# ls
node_exporter-1.4.0.linux-amd64.tar.gz  prometheus-2.40.2.linux-amd64
root@prometheus:~# tar xvfz node_exporter-1.4.0.linux-amd64.tar.gz
node_exporter-1.4.0.linux-amd64/
node_exporter-1.4.0.linux-amd64/LICENSE
node_exporter-1.4.0.linux-amd64/NOTICE
node_exporter-1.4.0.linux-amd64/node_exporter
root@prometheus:~# ls
node_exporter-1.4.0.linux-amd64  node_exporter-1.4.0.linux-amd64.tar.gz  prometheus-2.40.2.linux-amd64
root@prometheus:~# cd node_exporter-1.4.0.linux-amd64
root@prometheus:~/node_exporter-1.4.0.linux-amd64# ls
LICENSE  node_exporter  NOTICE
root@prometheus:~/node_exporter-1.4.0.linux-amd64# ./node_exporter
ts=2025-01-11T11:17:10.688Z caller=node_exporter.go:182 level=info msg="Starting node_exporter" version="(version=1.4.0, branch=HEAD, revision=7da1321761b3b8dfc9e496e1a60e6a476fec6018)"
ts=2025-01-11T11:17:10.688Z caller=node_exporter.go:183 level=info msg="Build context" build_context="(go=go1.19.1, user=root@83d90983e89c, date=20220926-12:32:56)"
ts=2025-01-11T11:17:10.688Z caller=node_exporter.go:185 level=warn msg="Node Exporter is running as root user. This exporter is designed to run as unprivileged user, root is not required."
ts=2025-01-11T11:17:10.689Z caller=filesystem_common.go:111 level=info collector=filesystem msg="Parsed flag --collector.filesystem.mount-points-exclude" flag=^/(dev|proc|run/credentials/.+|sys|var/lib/docker/.+|var/lib/containers/storage/.+)($|/)
ts=2025-01-11T11:17:10.689Z caller=filesystem_common.go:113 level=info collector=filesystem msg="Parsed flag --collector.filesystem.fs-types-exclude" flag=^(autofs|binfmt_misc|bpf|cgroup2?|configfs|debugfs|devpts|devtmpfs|fusectl|hugetlbfs|iso9660|mqueue|nsfs|overlay|proc|procfs|pstore|rpc_pipefs|securityfs|selinuxfs|squashfs|sysfs|tracefs)$
ts=2025-01-11T11:17:10.689Z caller=diskstats_common.go:100 level=info collector=diskstats msg="Parsed flag --collector.diskstats.device-exclude" flag=^(ram|loop|fd|(h|s|v|xv)d[a-z]|nvme\d+n\d+p)\d+$
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:108 level=info msg="Enabled collectors"
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=arp
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=bcache
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=bonding
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=btrfs
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=conntrack
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=cpu
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=cpufreq
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=diskstats
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=dmi
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=edac
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=entropy
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=fibrechannel
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=filefd
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=filesystem
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=hwmon
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=infiniband
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=ipvs
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=loadavg
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=mdadm
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=meminfo
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=netclass
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=netdev
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=netstat
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=nfs
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=nfsd
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=nvme
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=os
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=powersupplyclass
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=pressure
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=rapl
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=schedstat
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=selinux
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=sockstat
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=softnet
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=stat
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=tapestats
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=textfile
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=thermal_zone
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=time
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=timex
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=udp_queues
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=uname
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=vmstat
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=xfs
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:115 level=info collector=zfs
ts=2025-01-11T11:17:10.689Z caller=node_exporter.go:199 level=info msg="Listening on" address=:9100
ts=2025-01-11T11:17:10.690Z caller=tls_config.go:195 level=info msg="TLS is disabled." http2=false
^C
root@prometheus:~/node_exporter-1.4.0.linux-amd64# mkdir /etc/prometheus/node-exporter
root@prometheus:~/node_exporter-1.4.0.linux-amd64# cp ./node_exporter /etc/prometheus/node-exporter/
root@prometheus:~/node_exporter-1.4.0.linux-amd64# chorn -R prometheus:prometheus /etc/prometheus/node-exporter/
bash: chorn: команда не найдена
root@prometheus:~/node_exporter-1.4.0.linux-amd64# chown -R prometheus:prometheus /etc/prometheus/node-exporter/
root@prometheus:~/node_exporter-1.4.0.linux-amd64# ls -l /etc/prometheus/node-exporter/
итого 19184
-rwxr-xr-x 1 prometheus prometheus 19640886 янв 11 14:19 node_exporter
root@prometheus:~/node_exporter-1.4.0.linux-amd64# ls -al /etc/ | grep prometheus
drwxr-xr-x  5 prometheus prometheus  4096 янв 11 14:19 prometheus
root@prometheus:~/node_exporter-1.4.0.linux-amd64# nano /etc/systemd/system/node-exporter.service
root@prometheus:~/node_exporter-1.4.0.linux-amd64# pwd
/root/node_exporter-1.4.0.linux-amd64
root@prometheus:~/node_exporter-1.4.0.linux-amd64# systemctl enable node-exporter.service
Created symlink /etc/systemd/system/multi-user.target.wants/node-exporter.service → /etc/systemd/system/node-exporter.service.
root@prometheus:~/node_exporter-1.4.0.linux-amd64# systemctl start node-exporter.service
root@prometheus:~/node_exporter-1.4.0.linux-amd64# systemctl status node-exporter.service
● node-exporter.service - Node Exporter Lesson 9.4
     Loaded: loaded (/etc/systemd/system/node-exporter.service; enabled; preset: enabled)
     Active: active (running) since Sat 2025-01-11 14:34:58 MSK; 4s ago
   Main PID: 1119 (node_exporter)
      Tasks: 6 (limit: 4640)
     Memory: 4.8M
        CPU: 6ms
     CGroup: /system.slice/node-exporter.service
             └─1119 /etc/prometheus/node-exporter/node_exporter

янв 11 14:34:58 prometheus node_exporter[1119]: ts=2025-01-11T11:34:58.756Z caller=node_exporter.go:115 level=info collector>
янв 11 14:34:58 prometheus node_exporter[1119]: ts=2025-01-11T11:34:58.756Z caller=node_exporter.go:115 level=info collector>
янв 11 14:34:58 prometheus node_exporter[1119]: ts=2025-01-11T11:34:58.756Z caller=node_exporter.go:115 level=info collector>
янв 11 14:34:58 prometheus node_exporter[1119]: ts=2025-01-11T11:34:58.756Z caller=node_exporter.go:115 level=info collector>
янв 11 14:34:58 prometheus node_exporter[1119]: ts=2025-01-11T11:34:58.756Z caller=node_exporter.go:115 level=info collector>
янв 11 14:34:58 prometheus node_exporter[1119]: ts=2025-01-11T11:34:58.756Z caller=node_exporter.go:115 level=info collector>
янв 11 14:34:58 prometheus node_exporter[1119]: ts=2025-01-11T11:34:58.756Z caller=node_exporter.go:115 level=info collector>
янв 11 14:34:58 prometheus node_exporter[1119]: ts=2025-01-11T11:34:58.756Z caller=node_exporter.go:115 level=info collector>
янв 11 14:34:58 prometheus node_exporter[1119]: ts=2025-01-11T11:34:58.756Z caller=node_exporter.go:199 level=info msg="List>
янв 11 14:34:58 prometheus node_exporter[1119]: ts=2025-01-11T11:34:58.757Z caller=tls_config.go:195 level=info msg="TLS is >
lines 1-20/20 (END)
^C
root@prometheus:~/node_exporter-1.4.0.linux-amd64# ss -tlnp
State           Recv-Q          Send-Q                    Local Address:Port                      Peer Address:Port          Process
LISTEN          0               244                           127.0.0.1:5432                           0.0.0.0:*              users:(("postgres",pid=538,fd=6))
LISTEN          0               4096                            0.0.0.0:10050                          0.0.0.0:*              users:(("zabbix_agentd",pid=537,fd=4),("zabbix_agentd",pid=536,fd=4),("zabbix_agentd",pid=535,fd=4),("zabbix_agentd",pid=534,fd=4),("zabbix_agentd",pid=533,fd=4),("zabbix_agentd",pid=532,fd=4),("zabbix_agentd",pid=531,fd=4),("zabbix_agentd",pid=530,fd=4),("zabbix_agentd",pid=529,fd=4),("zabbix_agentd",pid=528,fd=4),("zabbix_agentd",pid=527,fd=4),("zabbix_agentd",pid=526,fd=4),("zabbix_agentd",pid=525,fd=4))
LISTEN          0               128                             0.0.0.0:22                             0.0.0.0:*              users:(("sshd",pid=519,fd=3))
LISTEN          0               4096                               [::]:10050                             [::]:*              users:(("zabbix_agentd",pid=537,fd=5),("zabbix_agentd",pid=536,fd=5),("zabbix_agentd",pid=535,fd=5),("zabbix_agentd",pid=534,fd=5),("zabbix_agentd",pid=533,fd=5),("zabbix_agentd",pid=532,fd=5),("zabbix_agentd",pid=531,fd=5),("zabbix_agentd",pid=530,fd=5),("zabbix_agentd",pid=529,fd=5),("zabbix_agentd",pid=528,fd=5),("zabbix_agentd",pid=527,fd=5),("zabbix_agentd",pid=526,fd=5),("zabbix_agentd",pid=525,fd=5))
LISTEN          0               244                               [::1]:5432                              [::]:*              users:(("postgres",pid=538,fd=5))
LISTEN          0               511                                   *:80                                   *:*              users:(("apache2",pid=550,fd=4),("apache2",pid=549,fd=4),("apache2",pid=548,fd=4),("apache2",pid=547,fd=4),("apache2",pid=546,fd=4),("apache2",pid=539,fd=4))
LISTEN          0               128                                [::]:22                                [::]:*              users:(("sshd",pid=519,fd=4))
LISTEN          0               4096                                  *:9100                                 *:*              users:(("node_exporter",pid=1119,fd=3))
LISTEN          0               4096                                  *:9090                                 *:*              users:(("prometheus",pid=956,fd=7))
root@prometheus:~/node_exporter-1.4.0.linux-amd64# nano /etc/prometheus/prometheus.yml
root@prometheus:~/node_exporter-1.4.0.linux-amd64# systemctl restart prometheus.service
root@prometheus:~/node_exporter-1.4.0.linux-amd64# systemctl status prometheus.service
● prometheus.service - Prometheus Service Netology Lesson 9.4
     Loaded: loaded (/etc/systemd/system/prometheus.service; enabled; preset: enabled)
     Active: active (running) since Sat 2025-01-11 14:38:00 MSK; 4s ago
   Main PID: 1143 (prometheus)
      Tasks: 9 (limit: 4640)
     Memory: 26.0M
        CPU: 61ms
     CGroup: /system.slice/prometheus.service
             └─1143 /usr/local/bin/prometheus --config.file /etc/prometheus/prometheus.yml --storage.tsdb.path /var/lib/prom>

янв 11 14:38:00 prometheus prometheus[1143]: ts=2025-01-11T11:38:00.274Z caller=head.go:683 level=info component=tsdb msg="W>
янв 11 14:38:00 prometheus prometheus[1143]: ts=2025-01-11T11:38:00.277Z caller=head.go:683 level=info component=tsdb msg="W>
янв 11 14:38:00 prometheus prometheus[1143]: ts=2025-01-11T11:38:00.277Z caller=head.go:683 level=info component=tsdb msg="W>
янв 11 14:38:00 prometheus prometheus[1143]: ts=2025-01-11T11:38:00.277Z caller=head.go:720 level=info component=tsdb msg="W>
янв 11 14:38:00 prometheus prometheus[1143]: ts=2025-01-11T11:38:00.278Z caller=main.go:1014 level=info fs_type=EXT4_SUPER_M>
янв 11 14:38:00 prometheus prometheus[1143]: ts=2025-01-11T11:38:00.278Z caller=main.go:1017 level=info msg="TSDB started"
янв 11 14:38:00 prometheus prometheus[1143]: ts=2025-01-11T11:38:00.278Z caller=main.go:1197 level=info msg="Loading configu>
янв 11 14:38:00 prometheus prometheus[1143]: ts=2025-01-11T11:38:00.278Z caller=main.go:1234 level=info msg="Completed loadi>
янв 11 14:38:00 prometheus prometheus[1143]: ts=2025-01-11T11:38:00.278Z caller=main.go:978 level=info msg="Server is ready >
янв 11 14:38:00 prometheus prometheus[1143]: ts=2025-01-11T11:38:00.278Z caller=manager.go:944 level=info component="rule ma>
lines 1-20/20 (END)
^C
root@prometheus:~/node_exporter-1.4.0.linux-amd64# sudo apt-get install -y adduser libfontconfig1 musl
Чтение списков пакетов… Готово
Построение дерева зависимостей… Готово
Чтение информации о состоянии… Готово
Уже установлен пакет adduser самой новой версии (3.134).
Уже установлен пакет libfontconfig1 самой новой версии (2.14.1-4).
libfontconfig1 помечен как установленный вручную.
Следующие НОВЫЕ пакеты будут установлены:
  musl
Обновлено 0 пакетов, установлено 1 новых пакетов, для удаления отмечено 0 пакетов, и 0 пакетов не обновлено.
Необходимо скачать 406 kB архивов.
После данной операции объём занятого дискового пространства возрастёт на 777 kB.
Пол:1 http://deb.debian.org/debian bookworm/main amd64 musl amd64 1.2.3-1 [406 kB]
Получено 406 kB за 0с (1 255 kB/s)
Выбор ранее не выбранного пакета musl:amd64.
(Чтение базы данных … на данный момент установлено 41214 файлов и каталогов.)
Подготовка к распаковке …/musl_1.2.3-1_amd64.deb …
Распаковывается musl:amd64 (1.2.3-1) …
Настраивается пакет musl:amd64 (1.2.3-1) …
Обрабатываются триггеры для man-db (2.11.2-2) …
root@prometheus:~/node_exporter-1.4.0.linux-amd64# wget https://dl.grafana.com/oss/release/grafana_9.2.5_amd64.deb
--2025-01-11 14:41:55--  https://dl.grafana.com/oss/release/grafana_9.2.5_amd64.deb
Распознаётся dl.grafana.com (dl.grafana.com)… 146.75.118.217, 2a04:4e42:8d::729
Подключение к dl.grafana.com (dl.grafana.com)|146.75.118.217|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 200 OK
Длина: 96671718 (92M) [application/octet-stream]
Сохранение в: «grafana_9.2.5_amd64.deb»

grafana_9.2.5_amd64.deb         100%[====================================================>]  92,19M  7,64MB/s    за 13s

2025-01-11 14:42:12 (7,36 MB/s) - «grafana_9.2.5_amd64.deb» сохранён [96671718/96671718]

root@prometheus:~/node_exporter-1.4.0.linux-amd64# ls
grafana_9.2.5_amd64.deb  LICENSE  node_exporter  NOTICE
root@prometheus:~/node_exporter-1.4.0.linux-amd64# pwd
/root/node_exporter-1.4.0.linux-amd64
root@prometheus:~/node_exporter-1.4.0.linux-amd64# sudo dpkg -i grafana_9.2.5_amd64.deb
Выбор ранее не выбранного пакета grafana.
(Чтение базы данных … на данный момент установлено 41228 файлов и каталогов.)
Подготовка к распаковке grafana_9.2.5_amd64.deb …
Распаковывается grafana (9.2.5) …
Настраивается пакет grafana (9.2.5) …
Добавляется системный пользователь «grafana» (UID 105) ...
Добавляется новый пользователь «grafana» (UID 105) в группу «grafana» ...
Не создаётся домашний каталог «/usr/share/grafana».
### NOT starting on installation, please execute the following statements to configure grafana to start automatically using systemd
 sudo /bin/systemctl daemon-reload
 sudo /bin/systemctl enable grafana-server
### You can start grafana-server by executing
 sudo /bin/systemctl start grafana-server
root@prometheus:~/node_exporter-1.4.0.linux-amd64# systemctl status grafana
Unit grafana.service could not be found.
root@prometheus:~/node_exporter-1.4.0.linux-amd64# systemctl status grafana.service
Unit grafana.service could not be found.
root@prometheus:~/node_exporter-1.4.0.linux-amd64# systemctl status grafana-server.service
○ grafana-server.service - Grafana instance
     Loaded: loaded (/lib/systemd/system/grafana-server.service; disabled; preset: enabled)
     Active: inactive (dead)
       Docs: http://docs.grafana.org
root@prometheus:~/node_exporter-1.4.0.linux-amd64# systemctl enable grafana-server.service
Synchronizing state of grafana-server.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable grafana-server
Created symlink /etc/systemd/system/multi-user.target.wants/grafana-server.service → /lib/systemd/system/grafana-server.service.
root@prometheus:~/node_exporter-1.4.0.linux-amd64# systemctl start grafana-server.service
root@prometheus:~/node_exporter-1.4.0.linux-amd64# systemctl status grafana-server.service
● grafana-server.service - Grafana instance
     Loaded: loaded (/lib/systemd/system/grafana-server.service; enabled; preset: enabled)
     Active: active (running) since Sat 2025-01-11 14:44:06 MSK; 3s ago
       Docs: http://docs.grafana.org
   Main PID: 1457 (grafana-server)
      Tasks: 8 (limit: 4640)
     Memory: 23.4M
        CPU: 133ms
     CGroup: /system.slice/grafana-server.service
             └─1457 /usr/sbin/grafana-server --config=/etc/grafana/grafana.ini --pidfile=/run/grafana/grafana-server.pid --p>

янв 11 14:44:09 prometheus grafana-server[1457]: logger=migrator t=2025-01-11T14:44:09.495538272+03:00 level=info msg="Execu>
янв 11 14:44:09 prometheus grafana-server[1457]: logger=migrator t=2025-01-11T14:44:09.671067934+03:00 level=info msg="Execu>
янв 11 14:44:09 prometheus grafana-server[1457]: logger=migrator t=2025-01-11T14:44:09.76308222+03:00 level=info msg="Execut>
янв 11 14:44:09 prometheus grafana-server[1457]: logger=migrator t=2025-01-11T14:44:09.855233448+03:00 level=info msg="Execu>
янв 11 14:44:09 prometheus grafana-server[1457]: logger=migrator t=2025-01-11T14:44:09.9634928+03:00 level=info msg="Executi>
янв 11 14:44:10 prometheus grafana-server[1457]: logger=migrator t=2025-01-11T14:44:10.055787255+03:00 level=info msg="Execu>
янв 11 14:44:10 prometheus grafana-server[1457]: logger=migrator t=2025-01-11T14:44:10.156026933+03:00 level=info msg="Execu>
янв 11 14:44:10 prometheus grafana-server[1457]: logger=migrator t=2025-01-11T14:44:10.281185198+03:00 level=info msg="Execu>
янв 11 14:44:10 prometheus grafana-server[1457]: logger=migrator t=2025-01-11T14:44:10.389804257+03:00 level=info msg="Execu>
янв 11 14:44:10 prometheus grafana-server[1457]: logger=migrator t=2025-01-11T14:44:10.498178909+03:00 level=info msg="Execu>

root@prometheus:~/node_exporter-1.4.0.linux-amd64# ^C
root@prometheus:~/node_exporter-1.4.0.linux-amd64# ss -tlnp
State           Recv-Q          Send-Q                    Local Address:Port                      Peer Address:Port          Process
LISTEN          0               244                           127.0.0.1:5432                           0.0.0.0:*              users:(("postgres",pid=538,fd=6))
LISTEN          0               4096                            0.0.0.0:10050                          0.0.0.0:*              users:(("zabbix_agentd",pid=537,fd=4),("zabbix_agentd",pid=536,fd=4),("zabbix_agentd",pid=535,fd=4),("zabbix_agentd",pid=534,fd=4),("zabbix_agentd",pid=533,fd=4),("zabbix_agentd",pid=532,fd=4),("zabbix_agentd",pid=531,fd=4),("zabbix_agentd",pid=530,fd=4),("zabbix_agentd",pid=529,fd=4),("zabbix_agentd",pid=528,fd=4),("zabbix_agentd",pid=527,fd=4),("zabbix_agentd",pid=526,fd=4),("zabbix_agentd",pid=525,fd=4))
LISTEN          0               128                             0.0.0.0:22                             0.0.0.0:*              users:(("sshd",pid=519,fd=3))
LISTEN          0               4096                               [::]:10050                             [::]:*              users:(("zabbix_agentd",pid=537,fd=5),("zabbix_agentd",pid=536,fd=5),("zabbix_agentd",pid=535,fd=5),("zabbix_agentd",pid=534,fd=5),("zabbix_agentd",pid=533,fd=5),("zabbix_agentd",pid=532,fd=5),("zabbix_agentd",pid=531,fd=5),("zabbix_agentd",pid=530,fd=5),("zabbix_agentd",pid=529,fd=5),("zabbix_agentd",pid=528,fd=5),("zabbix_agentd",pid=527,fd=5),("zabbix_agentd",pid=526,fd=5),("zabbix_agentd",pid=525,fd=5))
LISTEN          0               244                               [::1]:5432                              [::]:*              users:(("postgres",pid=538,fd=5))
LISTEN          0               511                                   *:80                                   *:*              users:(("apache2",pid=550,fd=4),("apache2",pid=549,fd=4),("apache2",pid=548,fd=4),("apache2",pid=547,fd=4),("apache2",pid=546,fd=4),("apache2",pid=539,fd=4))
LISTEN          0               128                                [::]:22                                [::]:*              users:(("sshd",pid=519,fd=4))
LISTEN          0               4096                                  *:9100                                 *:*              users:(("node_exporter",pid=1119,fd=3))
LISTEN          0               4096                                  *:9090                                 *:*              users:(("prometheus",pid=1143,fd=7))
root@prometheus:~/node_exporter-1.4.0.linux-amd64# ^C
root@prometheus:~/node_exporter-1.4.0.linux-amd64#
```