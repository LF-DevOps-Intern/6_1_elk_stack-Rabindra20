## B.   Collect metric from following sources in server1 and send them to elasticsearch. Store them in an index named "server1-metrics".
    a. Memory usage
    b. Disk usage
    c. Load average
Steps:-<br/>
There is two way to send data to elasticsearch <br/>
1. Install Metricbeat on the Elastic Stack server and import all the needed data, then install and configure the client on the second Ubuntu server.
2. Install and configure the client on the second Ubuntu server and Create index manually in kibana webpage

Installing and Configuring the metricbeat<br/>
Install the remaining components of the Elastic Stack using apt<br/>
Run apt-get update, and the repository is ready for use. For example, you can install Metricbeat by running<br/>
```
sudo apt-get update && sudo apt-get install metricbeat
```
![install](https://user-images.githubusercontent.com/53372486/144089537-33dbac26-7289-4cd7-993a-3d62655c9537.png)<br/>

Check system.yml<br/>
```
sudo nano /etc/metricbeat/modules.d/system.yml
```
![systemyml](https://user-images.githubusercontent.com/53372486/144186194-4834b446-d5e1-4643-a964-d3cde604ab69.png)<br/>

Edit metricbeat.yml file<br/>
```
/etc/metricbeat/metricbeat.yml
```
Add below lines in metricbeat.yml<br/>
```
hosts: ["192.168.141.128:9200"]
elasticsearch.username: "kibana_system"
elasticsearch.password: "Rabindra@1"
```
![yml copy](https://user-images.githubusercontent.com/53372486/144082331-b364b24e-23fe-429e-b9bc-47a096f21a58.png)<br/>

To load the index template into Elasticsearch. An Elasticsearch index is a collection of documents that have similar characteristics. Specific names identify each index, which Elasticsearch will use to refer to the indexes when performing various operations. Your Elasticsearch server will automatically apply the index template when you create a new index.<br/>
```
sudo metricbeat setup --template -E 'output.elasticsearch.hosts=["192.168.141.128:9200"]'
```
![index setup](https://user-images.githubusercontent.com/53372486/144089565-31fbc8a3-eff1-487c-bf60-43790359627a.png)<br/>

Metricbeat comes packaged with example Kibana dashboards, visualizations, and searches for visualizing Metricbeat data in Kibana<br/>
```
sudo metricbeat setup -e -E output.elasticsearch.hosts=['192.168.141.128:9200'] -E setup.kibana.host=192.168.141.128:5601
```
![setup](https://user-images.githubusercontent.com/53372486/144089544-02be93ce-1e70-4327-a75d-f36354fcb95d.png)<br/>

Start metricbeat<br/>
```
sudo systemctl enable metricbeat

sudo systemctl start metricbeat

sudo systemctl status metricbeat
```
![status](https://user-images.githubusercontent.com/53372486/144089552-84ea01b1-d93a-4301-b9d1-eecab744f8b9.png)<br/>

Click on discovery to view data in webpage<br/>

![data](https://user-images.githubusercontent.com/53372486/144166576-4bfd8f8c-dccf-4c47-b511-78ed8df083f1.png)<br/>

click on stream > add rule <br/>

![datastream](https://user-images.githubusercontent.com/53372486/144184085-b7168c3a-3cac-443c-8e80-d20ba388234d.png)<br/>











