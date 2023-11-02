# json_exporter_alertmanager
Scraping Alertmanager API to prometheus
Check api is working:
curl  http://localhost:9093/alertmanager/api/v2/alerts |jq

Download andi install json_exporter
wget https://github.com/prometheus-community/json_exporter/releases/download/v0.6.0/json_exporter-0.6.0.linux-amd64.tar.gz
tar xf json_exporter-0.6.0.linux-amd64.tar.gz
mv json_exporter-0.6.0.linux-amd64/json_exporter /usr/local/sbin/
chmod +x  /usr/local/sbin/json_exporter

