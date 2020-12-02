## Incializar el servicio 
```bash
 docker run \
 	--hostname=quickstart.cloudera \
 	--privileged=true  \
 	-it  \
 	-v $PWD:/src  \
 	--publish-all=true  \
 	-p 8888:8888  \
 	-p 8080:80  \
 	-p 7180:7180  \
 	-p 3306:3306  \
 	cloudera/quickstart  \
 	/usr/bin/docker-quickstart 
```
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
