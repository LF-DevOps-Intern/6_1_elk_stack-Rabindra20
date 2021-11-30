## B.   Collect metric from following sources in server1 and send them to elasticsearch. Store them in an index named "server1-metrics".
    a. Memory usage
    b. Disk usage
    c. Load average
Steps:-<br/>
There is two way to send data to elasticsearch <br/>
1. Install Metricbeat on the Elastic Stack server and import all the needed data, then install and configure the client on the second Ubuntu server.
2. Create yml file in server2 with all module and send data to elasticsearch through output plugin

Installing and Configuring the metricbeat<br/>
Install the remaining components of the Elastic Stack using apt<br/>
Run apt-get update, and the repository is ready for use. For example, you can install Metricbeat by running<br/>
```
sudo apt-get update && sudo apt-get install metricbeat
```
![install](https://user-images.githubusercontent.com/53372486/144089537-33dbac26-7289-4cd7-993a-3d62655c9537.png)<br/>

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

To load the index template into Elasticsearch. An Elasticsearch index is a collection of documents that have similar characteristics. Specific names identify each index, which Elasticsearch will use to refer to the indexes when performing various operations. Your Elasticsearch server will automatically apply the index template when you create a new index.<br/>
```
sudo metricbeat setup --template -E 'output.elasticsearch.hosts=["192.168.141.128:9200"]'
```
![setup](https://user-images.githubusercontent.com/53372486/144089544-02be93ce-1e70-4327-a75d-f36354fcb95d.png)<br/>

Metricbeat comes packaged with example Kibana dashboards, visualizations, and searches for visualizing Metricbeat data in Kibana<br/>
```
sudo metricbeat setup -e -E output.elasticsearch.hosts=['192.168.141.128:9200'] -E setup.kibana.host=192.168.141.128:5601
```
![index setup](https://user-images.githubusercontent.com/53372486/144089565-31fbc8a3-eff1-487c-bf60-43790359627a.png)<br/>

Start metricbeat<br/>
```
sudo systemctl enable metricbeat

sudo systemctl start metricbeat

sudo systemctl status metricbeat
```
![status](https://user-images.githubusercontent.com/53372486/144089552-84ea01b1-d93a-4301-b9d1-eecab744f8b9.png)<br/>











