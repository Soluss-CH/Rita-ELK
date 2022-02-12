# Rita-ELK

<p align="center"><img src="https://github.com/Soluss-CH/Rita-ELK/blob/main/Screenshot/Rita-Screen-General.png" width="400px"></p>

Rita-ELK is an integration of RITA logs in Elastic Stack.

Introduction
===============

What is RITA?
-------------

RITA is an open source framework for network traffic analysis.
The framework ingests Zeek Logs with the following major features:
- Beaconing Detection: Search for signs of beaconing behavior in and out of your network.
- DNS Tunneling Detection Search for signs of DNS based covert channels.
- Blacklist Checking: Query blacklists to search for suspicious domains and hosts.

More information on RITA: <a href="https://github.com/activecm/rita">RITA Github repository</a>.


Why this project?
-------------

RITA works on the command line. We wanted to have an interface to visualize the data and to have a continuous follow-up.


What are the features of this project?
-------------

- [X] [Hourly Zeek log analysis with Rita](https://github.com/Soluss-CH/Rita-ELK/blob/master/Rita/rita.cron)
- [X] [Data ingestion with Logstash](https://github.com/Soluss-CH/Rita-ELK/blob/master/Logstash/)
- [X] Rita Beacon logs parsing
- [X] Rita Long connection logs parsing
- [X] Rita DNS Tunnel logs parsing
- [X] [Visualization with Kibana](https://github.com/Soluss-CH/Rita-ELK/blob/master/Kibana/rita_dashboards.ndjson)




What does it look like?
-------------

### General dashboard
<p align="center"><img src="https://github.com/Soluss-CH/Rita-ELK/blob/main/Screenshot/Rita-Screen-General.png" width="400px"></p>


### Beacon dashboard
<p align="center"><img src="https://github.com/Soluss-CH/Rita-ELK/blob/main/Screenshot/Rita-Screen-Beacon.png" width="400px"></p>


### DNS Tunnel dashboard
<p align="center"><img src="https://github.com/Soluss-CH/Rita-ELK/blob/main/Screenshot/Rita-Screen-DNS.png" width="400px"></p>


### Long connection dashboard
<p align="center"><img src="https://github.com/Soluss-CH/Rita-ELK/blob/main/Screenshot/Rita-Screen-Long.png" width="400px"></p>



Getting Started
===============
Requirements
-------------
1) Rita, Zeek and MongoDB installed. A detailed process is available <a href="https://github.com/activecm/rita/blob/master/docs/Manual%20Installation.md">here</a>.
2) An Elastic stack installed with Logstash, Elasticsearch, Kibana. A detailed process is available <a href="https://www.elastic.co/guide/index.html">here</a>.


Installation
-------------

1) Install the index template in Elasticsearch: sudo curl -X PUT https://username:password@hostname:9200/_template/template-rita -H 'Content-Type: application/json' --data-binary "@./Elasticsearch/template-rita.json"  -k
2) Import dashboard in Kibana: sudo curl -X POST https://user:password@hostname:5601/api/saved_objects/_import?createNewCopies=true -H "kbn-xsrf: true" --form file="@./Kibana/rita_dashboards.ndjson" -H 'kbn-xsrf: true' -k
3) Copy the cron file to hourly parse zeek logs: sudo cp ./Rita/rita.cron /etc/cron.d/
4) Copy Logstash configuration files cp ./Logstash/* /etc/logstash/conf.d/
5) Edit 10-rita_filter.conf to setup your output accordigly to your Elasticsearch (username, password, hostname, certificate).