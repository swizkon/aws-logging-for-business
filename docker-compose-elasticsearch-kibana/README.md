# docker-compose-elasticsearch-kibana

## Overview
Docker Compose for 3 Node Elasticsearch (6.5.0) Cluster and Kibana (Open Source 6.5.0) Instance for development purposes.

Kibana is being served behind Nginx Proxy so you can secure access of kibana for your purpose.

## Requirements
1. Docker 18.05
2. Docker-compose 1.21

### Start Stack in Daemon Mode
```
docker-compose up -d
```

### Check status of docker-compose cluster
```
docker-compose ps -a
```

### Cluster Node Info
```
curl http://localhost:9200/_nodes?pretty=true
```

### Access Kibana
```
http://localhost:5601
```

### Accessing Kibana through Nginx
```
http://localhost:8090
```

### Access Elasticsearch
```
http://localhost:9200
```

### Logstash
```
C:\Dev\logstash-7.1.1\bin>logstash -f ../config/logstash-sample.conf
```

### Run with single proc for elastic and kibana
```
docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" --rm --name myelasticsearch docker.elastic.co/elasticsearch/elasticsearch:6.5.0
docker run -d -p 5601:5601 -e "SERVER_NAME=localhost" -e "ELASTICSEARCH_URL=http://[IPFROM EALSTIC CONTAINER]:9200/" --rm --name mykibana docker.elastic.co/kibana/kibana-oss:6.5.0

docker run -it -p 5601:5601 -e "SERVER_NAME=localhost" -e "ELASTICSEARCH_URL=http://[IPFROM EALSTIC CONTAINER]:9200/" --rm --name mykibana docker.elastic.co/kibana/kibana-oss:6.5.0


docker run -it -p 5000:5000 -e "SERVER_NAME=localhost" -e "ELASTICSEARCH_URL=http://[IPFROM EALSTIC CONTAINER]:9200/" --rm --name mylogstash docker.elastic.co/logstash/logstash-oss:6.2.2

docker inspect -f {{.NetworkSettings.Gateway}} myelasticsearch

C:\Dev\logstash-7.1.1\bin\logstash -f C:\Dev\logstash-7.1.1\config\logstash-sample.conf


```

# Resources
* [Hands on Elasticsearch](https://medium.com/@maxy_ermayank/hands-on-elasticsearch-8fa59d8aebfc)
* [Elasticsearch Resources](https://medium.com/@maxy_ermayank/elasticsearch-resources-27d24f01c1dc)
