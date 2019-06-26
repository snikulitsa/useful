# ELASTIC
Key | Value
------- | --------
HOME | `/usr/share/elasticsearch`  
STOP_WORDS | `/etc/elasticsearch/elasticsearch/search_stop_words.txt`  
RUSSIAN_MORPHOLOGY | `https://github.com/imotov/elasticsearch-analysis-morphology`  
KIBANA_HOME | `/opt/kibana`
#### Installation
```bash
curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.6.13.deb
sudo dpkg -i elasticsearch-5.6.13.deb
sudo /etc/init.d/elasticsearch start
sudo systemctl enable elasticsearch.service
cd /ush/share/elasticsearch
sudo bin/elasticsearch-plugin install http://dl.bintray.com/content/imotov/elasticsearch-plugins/org/elasticsearch/elasticsearch-analysis-morphology/5.6.13/elasticsearch-analysis-morphology-5.6.13.zip
```
#### Allow remote connections
```bash
sudo mcedit /etc/elasticsearch/elasticsearch.yml
```
Set `network.host` IP address of elasticsearch host