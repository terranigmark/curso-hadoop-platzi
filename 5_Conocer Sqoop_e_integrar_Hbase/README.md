## Abrir hbase
```bash
hbase shell 
```
## Crear tabla

```bash
create 'newtbl', 'knowledge'

```
## Listar las tablas o documentos

```bash
list 
```
## Ver las caracteristicas de nuestra tabla o documento

```bash

describe 'newtbl'
```
```bash
status 'summary'

```
## Insertar datos en nuesta BD

```bash
put 'newtbl','r1','knowledge:books','Alicia en el pais de las maravillas'
```

```bash

put 'newtbl','r2','knowledge:books','Odisea'
```

## Revisar nuestros datos

```bash
scan 'newtbl'
```


# Importar solamente una tabla usando sqoop 

### Levantar nuestro ambiente de Hadoop

```bash
docker run \
    --hostname=quickstart.cloudera  \
    --network=platzi  \
    --privileged=true  \
    -it  \
    -v $PWD:/src  \
    --publish-all=true  \
    -p 8888:8888  \
    -p 8080:80  \
    -p 7180:7180  \
    cloudera/quickstart  \
    /usr/bin/docker-quickstart 
```

### Comando de Sqoop para importar solamente una tabla de una base de datos

```bash

sqoop import -m 1 \
		--connect jdbc:mysql://quickstart:3306/retail_db  \
		--username=retail_dba  \
		--password=cloudera  \
		--warehouse-dir=/user/hive/warehouse/  \
		--table customers  \
		--compression-codec=snappy  \
		--as-parquetfile --hive-import \
```

### Hacer una consulta rápida con Impala
```bash
invalidate metadata;
show tables;
select * from customers;
```


