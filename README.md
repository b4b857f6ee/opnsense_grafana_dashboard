# opnsense_grafana_dashboard
Grafana Dashboard for OPNsense and the Plugin Sensei

# Requirement

- ELK stack 7+
- Telegraf configuration for OPNsense
- Grafana and InfluxDB

# OPNsense configuration

- ELK logs, configure the ELK logs by following this : https://github.com/3ilson/pfelk
- Install Telegraf plugin and configure it to send metrics into InfluxDB

# Grafana configuration

- Configure the Datasource for InfluxDB
- Configuration of the pfelk Elasticsearch
	Datasources :
					Name : Elasticsearch-Firewall
					URL : yourELKIP:9200
					Index name : pfelk-firewall*
					Time field name : @timestamp
					Version : 7.0+
					
					Name : Elasticsearch-Suricata
					URL : yourELKIP:9200
					Index name : pfelk-suricata*
					Time field name : @timestamp
					Version : 7.0+
					
					Name : Elasticsearch-unbound
					URL : yourELKIP:9200
					Index name : pfelk-unbound*
					Time field name : @timestamp
					Version : 7.0+
					
					You can use the Name you want and filter it in the dashboard your import, in the Settings -> Variables -> Elasticsearch -> Adn modify the "Instance name filter" for exemple here for matching suricata : /.*Suricata.*/

Dashboard :
	InfluxDB : OPNSense - Firewall
	ELK : Firewall - Dashboard | Firewall - Suricata | Firewall - Unbound


# Configuration for Sensei Module https://docs.opnsense.org/vendor/sunnyvalley/sensei.html

Configure Sensei by using external ELK (like the one you have previously install) Or you can use the internal ELK who is install during the Sensei installation. Just configure a Port translation from your administration interface or OPNsense on the port 9200 to the 127.0.0.1:9200
- Configuration of the pfelk Elasticsearch
	Datasources :
					Name : Elasticsearch-Sensei
					URL : yourELKIP:9200
					Index name : *
					Time field name : start_time
					Version : 7.0+ Or 5.6+(for Internal OPNsense Sensei ELK)
