# Elastic Search Logstash & Kibana

https://www.docker.elastic.co/


### 1.- Crear la red 

```bash
docker network create -d bridge hadoopNet   
```
## 2.- Levantar el servicio de ElasticSearch

```bash
docker run \
-p 9200:9200 -p 9300:9300 \
--net=hadoopNet \
--name elasticsearch \
-e "discovery.type=single-node" \
docker.elastic.co/elasticsearch/elasticsearch:7.6.2
```

### 3.- Levantar el servicio de Logstash 
### 3.1 Hacer el archivo de configuración logstash.conf
```bash
mkdir pipeline
vim pipeline/logstash.conf
```

```bash
input {
 stdin {}
}

output {
  elasticsearch {
    hosts => ["elasticsearch:9200"]
  }
}
```
### 3.2 Levantar el servicio de Logstrash para terminal

```bash
docker run -it \
--rm \
--net=hadoopNet \
--name logstash \
-v "$PWD/pipeline":/app \
--entrypoint bash \
docker.elastic.co/logstash/logstash:7.6.2 
```
### 3.3 Cargar el archivo de configuración

```bash
logstash -f /app/logstash.conf
```
### 3.4.-  Revisar nuestros datos en

http://localhost:9200/_search?pretty&size=1000
 ó
```bash
 curl http://localhost:9200/_search?pretty&size=1000
```

### 4.- Levantar el servicio de Kibana 

```bash
docker run --rm \
--name kibana \
--net=hadoopNet \
-p 5601:5601 \
kibana:7.6.2
```

### 5.- Revisar nuestros servicios de ELK en la red hadoopNet
```bash
docker inspect hadoopNet
```

### 6.- Revisión transmisión de datos

```bash
curl http://localhost:9200/_cat/indices\?v
```
License
----

MIT


