##### 1. Crear red para el cluster de hadoop

```
sudo docker network create --driver=bridge hadoop
```

##### 2. Inicializar el cluster

```
cd 1_Crear_tu_propio_dockerfile_para_tu_entorno_de_pruebas_con_Hadoop
sudo ./start-container.sh
```

**output:**

```
start hadoop-master container...
start hadoop-slave1 container...
start hadoop-slave2 container...
root@hadoop-master:~# 
```
- Iniciar con 2  esclavos y un maestro
- Entraremos al contenedor master

##### 3. Iniciar hadoop

```
./start-hadoop.sh
```

##### 4. Un archivo txt de un libro

```
echo "texto para hadoop" > ejemplo.txt

```

##### 5. Crear un directorio en hadoop

```
hdfs dfs -mkdir -p platzi
```

##### 6. Crear un archivo tipo tar.gz

```
hdfs dfs -put ejemplo.txt platzi/
```


##### 7. Revisar los tamaños de nuestros archivos

```
hdfs dfs -ls platzi/
```

##### 9. Revisar nuestro input directorio en HADOOP

```
localhost:570
```
