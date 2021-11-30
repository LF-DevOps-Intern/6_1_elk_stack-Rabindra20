### A.  Create two linux servers,
#    server1 => install and configure kibana and elasticsearch with basic username and password authentication
#   server2 => install and configure metricbeat.
Steps:<br/>
Installing and Configuring Elasticsearch<br/>
Run the following command to import the Elasticsearch public GPG key into APT<br/>
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```
![wget](https://user-images.githubusercontent.com/53372486/144078556-8b908a84-bd67-4ac9-9c01-511605f92936.png)<br/>

Add the Elastic source list to the sources.list.d directory<br/>
```
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
```
![echo](https://user-images.githubusercontent.com/53372486/144078572-cd873e36-2cdc-4413-8c4e-edea575d6b56.png)<br/>

Update your package lists so APT will read the new Elastic source<br/>
```
sudo apt update
```
![apt](https://user-images.githubusercontent.com/53372486/144078563-729d3e0c-9392-456a-a0b7-8716d74efbe1.png)<br/>

install Elasticsearch with this command:<br/>
```
sudo apt install elasticsearch
```
![install](https://user-images.githubusercontent.com/53372486/144078576-d116f3d0-aad4-4c2f-92c9-a2624644ded5.png)<br/>

Configuration<br/>
Edit elacsearch.yml file<br/>
```
sudo nano /etc/elasticsearch/elacsearch.yml
```
And add network host<br/>
```
network.host:192.168.141.128
discovery.type: single-node
xpack.security.enabled: true
xpack.security.authc.api_key.enabled: true
```
![yml](https://user-images.githubusercontent.com/53372486/144078561-47c4ee2a-982c-4e3f-9e6e-827edc6aa033.png)<br/>

open elasticsearch bin to set password<br/>
Change dir<br/>
```
cd /usr/share/elasticsearch/bin
```
Run <br/>
```
sudo ./elasticsearch-setup-passwords interactive
```
![passwordset](https://user-images.githubusercontent.com/53372486/144078545-d1c3f240-527f-4172-a100-ff362463e22c.png)<br/>

Start elasticsearch<br/>
```
sudo systemctl start elasticsearch
```
Check status <br/>
```
sudo systemctl start elasticsearch
```
![status](https://user-images.githubusercontent.com/53372486/144078553-0c4b30cb-d773-42cd-9818-f74821d8067b.png)<br/>

Display<br/>
![display password](https://user-images.githubusercontent.com/53372486/144078564-f62eed3c-e574-4610-a8ee-dc8e76700366.png)<br/>
![display](https://user-images.githubusercontent.com/53372486/144078566-ae6f3029-2ec7-4ae6-a2be-6d1450dbbff0.png)<br/>
-----------------------------------------------------<br/>
Installing and Configuring the Kibana<br/>
Install the remaining components of the Elastic Stack using apt<br/>
```
sudo apt install kibana
```
![kibana](https://user-images.githubusercontent.com/53372486/144078582-f05e8e8d-63fd-4a29-9ba5-ad915b4685bd.png)<br/>

Edit kibana file<br/>
```
sudo nano /etc/kibana/kibana.yml
```
Add below lines in kibana.yml<br/>
```
server.host: "0.0.0.0"
elasticsearch.username: "kibana_system"
elasticsearch.password: "Rabindra@1"
```
Start kibana <br/>
```
sudo systemctl enable kibana

sudo systemctl start kibana
```
Check status<br/>
```
sudo systemctl status kibana
```
![kibana status](https://user-images.githubusercontent.com/53372486/144078579-8682d6ae-b888-481f-a4b2-ec54343219a6.png)<br/>

Display<br/>
![kibana web](https://user-images.githubusercontent.com/53372486/144078581-17a2ef61-4ec3-43bb-9e7a-87121d714ce2.png)<br/>

After configure with elasticsearch<br/>
![login](https://user-images.githubusercontent.com/53372486/144078584-5602373b-fa87-4438-ba65-0af66fc42668.png)<br/>
![home](https://user-images.githubusercontent.com/53372486/144078574-6b98c720-4b9d-4e0a-b77f-8501601eb588.png)<br/>

------------------------------------------------------<br/>
#   server2 => install and configure metricbeat.
Steps:-
Download and install the Public Signing Key:
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```
![wget](https://user-images.githubusercontent.com/53372486/144078556-8b908a84-bd67-4ac9-9c01-511605f92936.png)<br/>

Install the apt-transport-https package on Debian before proceeding:<br/>
```
sudo apt-get install apt-transport-https
```
![trans](https://user-images.githubusercontent.com/53372486/144083483-572cfa8f-990d-41db-aa99-cc90ad816784.png)<br/>

Save the repository definition to /etc/apt/sources.list.d/elastic-7.x.list:<br/>
```
echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
```
![stables](https://user-images.githubusercontent.com/53372486/144082346-076aef65-e5c8-4b35-b92d-cd4dafdcc5d1.png)<br/>

Run apt-get update, and the repository is ready for use. For example, you can install Metricbeat by running<br/>
```
sudo apt-get update && sudo apt-get install metricbeat
```
![install copy](https://user-images.githubusercontent.com/53372486/144082340-86227942-efcb-440d-866d-1f7a01fe2a40.png)<br/>

Edit metricbeat file<br/>
```
/etc/metricbeat/metricbeat.yml
```
Add below lines in kibana.yml<br/>
```
hosts: ["192.168.141.128:9200"]
elasticsearch.username: "kibana_system"
elasticsearch.password: "Rabindra@1"
```
![yml copy](https://user-images.githubusercontent.com/53372486/144082331-b364b24e-23fe-429e-b9bc-47a096f21a58.png)<br/>

set server2 name<br/>
```
sudo hostnamectl set-hostname server2
```
Start metricbeat<br/>
```
sudo systemctl enable metricbeat

sudo systemctl start metricbeat

sudo systemctl status metricbeat
```
![metricstatus](https://user-images.githubusercontent.com/53372486/144085468-9213271c-3df3-4013-9574-18926af09aa8.png)<br/>














