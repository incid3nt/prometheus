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

1.2 Скачаем node exporter
```
wget https://github.com/incid3nt/prometheus/blob/main/tar/node_exporter-1.4.0.linux-amd64.tar.gz
```
Распакуем:
```
tar xvfz node_exporter-1.4.0.linux-amd64.tar.gz
```
Создадим папку для node-exporter
```
mkdir /etc/prometheus/node-exporter
```
Скопируем:
```
cp ./node_exporter /etc/prometheus/node-exporter/
```
Выдаем права:
```
chown -R prometheus:prometheus /etc/prometheus/node-exporter/
```
1.3 Сервис для node-exporter
nano /etc/systemd/system/node-exporter.service
```
[Unit]
Description=Node Exporter Lesson 9.4 - [Еноктаев Олег Владимирович]
After=network.target
[Service]
User=prometheus
Group=prometheus
Type=simple
ExecStart=/etc/prometheus/node-exporter/node_exporter
[Install]
WantedBy=multi-user.target
```
Включаем , добавляем в автозагрузку:
```
systemctl enable node-exporter.service
systemctl start node-exporter.service
systemctl status node-exporter.service
```
1.4 

![nodeexporter](https://github.com/incid3nt/prometheus/blob/main/img/putty_BbZpC09M8t.png)

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 2](ссылка на скриншот 2)`


---

### Задание 3

Подключите Node Exporter к серверу Prometheus.

1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Отредактируйте prometheus.yaml, добавив в массив таргетов установленный в задании 2 node exporter
3. Перезапустите prometheus
4. Проверьте что он запустился

1.2 nano /etc/prometheus/prometheus.yml
```
# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
          # - alertmanager:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["localhost:9090", "localhost:9100"]
```
1.3 перезапустим prometheus
```
systemctl restart prometheus.service
```
1.4 Запущен:
![systemctl](https://github.com/incid3nt/prometheus/blob/main/img/putty_gG9QB4PZcc.png)

![node](https://github.com/incid3nt/prometheus/blob/main/img/chrome_OIsaHMhK5Q.png)
![node](https://github.com/incid3nt/prometheus/blob/main/img/chrome_QfZKZId6gd.png)
### Задание 4

Установите Grafana.

![grafana](https://github.com/incid3nt/prometheus/blob/main/img/chrome_shwZ0JtPAA.png)

### Задание 5

Интегрируйте Grafana и Prometheus.

![grafana](https://github.com/incid3nt/prometheus/blob/main/img/chrome_hQ9qyhCQv3.png)
![grafana](https://github.com/incid3nt/prometheus/blob/main/img/chrome_zlLOafjoal.png)