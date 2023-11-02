# json_exporter_alertmanager
Scraping Alertmanager API to prometheus
Check api is working:
  curl  http://localhost:9093/alertmanager/api/v2/alerts |jq

Download and install json_exporter as systemd unit:
  wget https://github.com/prometheus-community/json_exporter/releases/download/v0.6.0/json_exporter-0.6.0.linux-amd64.tar.gz
  tar xf json_exporter-0.6.0.linux-amd64.tar.gz
  mv json_exporter-0.6.0.linux-amd64/json_exporter /usr/local/sbin/
  chmod +x  /usr/local/sbin/json_exporter
  cp json_exporter.service /etc/systemd/system/json_exporter.service
  cp json_exporter /etc/default/json_exporter
  cp json_exporter.yml /etc/prometheus/json_exporter.yml
  systemctl daemon-reload
  systemctl enable json_exporter
  systemctl start json_exporter
  netstat -nltup |grep 7979

Copy code from prometheus.yml to your /etc/prometheus/prometheus.yml
check configuration:
promtool check config /etc/prometheus/prometheus.yml
reload prometheus
systemctl reload prometheus

check if its working:
curl "http://localhost:7979/probe?module=default&target=http://localhost:9093/alertmanager/api/v2/alerts"

prom query example:
sum(Alertmanager_scrape_status{alertname="PROD_OS_load15_above_cpu_count_for_1h"})
