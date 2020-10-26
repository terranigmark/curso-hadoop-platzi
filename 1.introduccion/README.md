
##### 1. pull docker image

```
sudo docker pull uracilo/hadoop
```

##### 2. Clonar repositorio github

```
git clone https://github.com/uracilo/hadoop.git
```

##### 3. Crear red para el cluster de hadoop

```
sudo docker network create --driver=bridge hadoop
```

##### 4. Inicializar el cluster

```
cd hadoop
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

##### 5. Iniciar hadoop

```
./start-hadoop.sh
```

##### 6. Un archivo txt de un libro

```
wget https://raw.githubusercontent.com/uracilo/testdata/master/odisea.txt
```

##### 7. Crear un directorio

```
mkdir input
```

##### 8. Crear un archivo tipo tar.gz

```
tar -czvf input/odisea.tar.gz odisea.txt
```

-c: Generar archivo
-z: Comprimir con gzip.
-v: Progreso del proceso.
-f: Especificar nombre del archivo.


##### 9. Revisar los tamaños de nuestros archivos

```
ls -flarts input
```
##### 10. Crear y mover  directorio input al DFS de  HADOOP

```
hdfs dfs -mkdir -p test
hdfs dfs -put input
```

##### 11. Revisar nuestro input directorio en HADOOP

```
hdfs dfs –ls  input
```

##### 12. Leer las primeras lineas de nuestro archivo en HADOOP

```
hdfs dfs -cat  input/odisea.tar.gz | zcat | tail -n 20
```

##### 13. Eliminar el archivo en HADOOP

```
hdfs dfs –rm –f /user/rawdata/example/odisea.tar.gz
```

##### Plus ejecutar un trabajo en HADOOP

```
hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/sources/hadoop-mapreduce-examples-2.7.2-sources.jar org.apache.hadoop.examples.WordCount input output
```

##### Plus ver el resultado del trabajo en HADOOP

```
hdfs dfs -cat output/part-r-00000
```