# Obtener un tsv comprimirlo a .gz de una base de datos relacional y hacer consultas en Hive

```bash
mysql -h 172.25.0.2 -u root --password=rootpwd -e "select * from db_name.user_details" -B > user_data.tsv
```
# Generar un archivo .gz

```bash
gzip user_data.tsv
```
# Correr nuestro ambiente de cloudera

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


# Mover nuestro archivo a HDFS

```bash
hdfs dfs -mkdir -p /user/cloudera/raw_data/
hdfs dfs -put *.gz /user/cloudera/raw_data/
hdfs dfs -ls /user/cloudera/raw_data/
```

# Interactuar con nuestro archivo en HIVE
```bash
CREATE DATABASE mysql_raw;

CREATE EXTERNAL TABLE IF NOT EXISTS 
mysql_raw.users_tsv(user_id INT, 
                 username STRING,
                 first_name STRING,
                 last_name STRING,
                 gender STRING,
                 password STRING,
                 status INT ) 
COMMENT 'users' ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' 
STORED AS textfile LOCATION '/user/cloudera/raw_data' TBLPROPERTIES ("skip.header.line.count"="1");
```

```bash
SHOW CREATE TABLE mysql_raw.users_tsv;
```

```bash
CREATE DATABASE mysql_master;
```

```bash
CREATE TABLE mysql_master.users STORED AS PARQUET LOCATION '/user/cloudera/raw_data/user_data.tsv.gz' TBLPROPERTIES ('PARQUET.COMPRESS'='SNAPPY') AS SELECT * FROM mysql_raw.users_tsv;
```

```bash
SHOW CREATE TABLE mysql_master.users;
```

```bash
SELECT * FROM mysql_master.users;
```























