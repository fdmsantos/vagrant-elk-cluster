# Vagrant ELK Cluster

**Not For use in Production**

ELK Cluster with Vagrant with 3 nodes

## Software versions information

| Software              | Version     | Description                        |
| --------------------------------- | ----------- | ----------------------------------------- |
| CentOS|7.5| Guest OS :[chef/centos-7.1](https://app.vagrantup.com/centos/boxes/7) |
| Java (oracle)              | 1.8.0_191    |     |
| ElasticSearch                     | 6.4.2       | [Reference Guide](https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html) / [Definitive Guide](https://www.elastic.co/guide/en/elasticsearch/guide/current/index.html) |
| Kibana | 6.4 | [Reference Guide](https://www.elastic.co/guide/en/kibana/current/index.html)|
| LogStash | Upcoming | - |


## Cluster Nodes

| Node Name | Node Ip | Description  |
| --- | ---- | --- |
|node1|172.17.9.101|Elasticsearch Master Node <br> Kibana |
|node2|172.17.9.102|Elasticsearch Data Node|
|node3|172.17.9.103|Elasticsearch Data Node|


## Urls

| Node Name | Node Ip | Description  |
| --- | ---- | --- |
|Elasticsearch|http://172.17.9.101:9200
|Kibana|http://172.17.9.101:5601

## Pre Requisite & Set up

**Must have on your host machine**

* VirtualBox
* Vagrant

**Setup**

```
git clone https://github.com/fdmsantos/vagrant-elk-cluster.git
cd vagrant-elk-cluster
vagrant up
```

## SSH to Nodes
```
cd vagrant-elk-cluster
vagrant ssh node1
vagrant ssh node2
vagrant ssh node3
```