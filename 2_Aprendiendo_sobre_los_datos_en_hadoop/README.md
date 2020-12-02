##### 1. Crear red para el cluster de hadoop

```
sudo docker network create --driver=bridge hadoop
```

##### 2. Inicializar el cluster

```
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

wget -b https://raw.githubusercontent.com/terranigmark/curso-hadoop-platzi/2_Aprendiendo_sobre_los_datos_en_hadoop/2_Aprendiendo_sobre_los_datos_en_hadoop/books/Alices_adventures.txt
wget -b https://raw.githubusercontent.com/terranigmark/curso-hadoop-platzi/2_Aprendiendo_sobre_los_datos_en_hadoop/2_Aprendiendo_sobre_los_datos_en_hadoop/books/SYMBOLIC_LOGIC.txt
wget -b https://raw.githubusercontent.com/terranigmark/curso-hadoop-platzi/2_Aprendiendo_sobre_los_datos_en_hadoop/2_Aprendiendo_sobre_los_datos_en_hadoop/books/the_hunting_of_snark.txt


rm -rf wget*
```

##### 5. Crear un directorio

```
mkdir input

```

##### 6. Crear un archivo tipo tar.gz

```
tar -czvf input/lewis.tar.gz *
```

-c: Generar archivo
-z: Comprimir con gzip.
-v: Progreso del proceso.
-f: Especificar nombre del archivo.


##### 7. Revisar los tamaños de nuestros archivos

```
ls -flarts input
```
##### 8. Crear y mover  directorio input al DFS de  HADOOP

```
hdfs dfs -mkdir -p test
hdfs dfs -mkdir -p input
hdfs dfs -put input/lewis.tar.gz
hdfs dfs -mv lewis.tar.gz input
hdfs dfs -ls 
```

##### 9. Revisar nuestro input directorio en HADOOP

```
hdfs dfs –ls  input
```

##### 10. Leer las primeras lineas de nuestro archivo en HADOOP

```
hdfs dfs -cat  input/odisea.tar.gz | zcat | tail -n 20
```

##### 11. Eliminar el archivo en HADOOP

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


Inspirado en https://github.com/kiwenlau/hadoop-cluster-docker
