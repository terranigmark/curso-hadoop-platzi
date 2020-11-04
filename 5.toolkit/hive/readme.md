Para IMPALA
invalidate metadata;
show tables;







-- Most popular product categories
select c.category_name, count(order_item_quantity) as count
from order_items oi
inner join products p on oi.order_item_product_id = p.product_id
inner join categories c on c.category_id = p.product_category_id
group by c.category_name
order by count desc
limit 10;






 curl http://localhost:9200/_search?pretty&size=1000




docker run --hostname=quickstart.cloudera --privileged=true -it -v $PWD:/src --publish-all=true -p 8888:8888 -p 8080:80 -p 7180:7180 cloudera/quickstart /usr/bin/docker-quickstart




sqoop import-all-tables \
    -m 1 \
    --connect jdbc:mysql://172.23.0.2:3306/db_name \
    --username=root \
    --password=rootpwd \
    --compression-codec=snappy \
    --as-parquetfile \
    --warehouse-dir=/user/hive/bookstore \
    --hive-import



sqoop import --conect jdbc:mysql://172.23.0.2:3306/db_name







docker run --hostname=quickstart.cloudera --privileged=true -it -v $PWD:/src --publish-all=true -p 8888:8888 -p 8080:80 -p 7180:7180 cloudera/quickstart /usr/bin/docker-quickstart







mongoexport --host 172.23.0.3 --db hadoop --collection elements --out elements.json --jsonArray

mongodump --host 172.23.0.3 --db hadoop --collection elements --out mongo_db 




mongoexport --host 172.25.0.3 --db hadoop --collection elements --type csv --fields=first_name,gender  --out names.csv










mysql -h 172.25.0.2 -u root --password=rootpwd -e "select * from db_name.user_details" -B > user_data.tsv






docker run --hostname=quickstart.cloudera --network=platzi --privileged=true -it -v $PWD:/src --publish-all=true -p 8888:8888 -p 8080:80 -p 7180:7180 cloudera/quickstart /usr/bin/docker-quickstart








mysql -uroot --password=rootpwd -h 172.25.0.2 -P 3306

gzip 


hdfs dfs -mkdir -p /user/cloudera/raw_data/
hdfs dfs -put *.gz /user/cloudera/raw_data/
hdfs dfs -ls /user/cloudera/raw_data/




CREATE DATABASE mysql_raw;

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
SHOW CREATE TABLE mysql_raw.users_tsv;
CREATE DATABASE mysql_master;
CREATE TABLE mysql_master.users STORED AS PARQUET LOCATION '/user/cloudera/raw_data/user_data.tsv.gz' TBLPROPERTIES ('PARQUET.COMPRESS'='SNAPPY') AS SELECT * FROM mysql_raw.users_tsv;
SHOW CREATE TABLE mysql_master.users;
SELECT * FROM mysql_master.users;

::::::::::::::::::::::::::::::::::::::::::::::::::::::::.





CREATE DATABASE mongo_raw;

CREATE EXTERNAL TABLE IF NOT EXISTS 
mongo_raw.users_csv(first_name STRING, 
                 gender STRING ) 
COMMENT 'users' ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
STORED AS textfile LOCATION '/user/cloudera/raw_data' TBLPROPERTIES ("skip.header.line.count"="1");

SHOW CREATE TABLE mongo_raw.users_csv;
CREATE DATABASE mongo_master;

CREATE TABLE mongo_master.users STORED AS AVRO LOCATION '/user/cloudera/raw_data/names.csv.gz' TBLPROPERTIES ('PARQUET.COMPRESS'='SNAPPY') AS SELECT * FROM mongo_raw.users_csv;

SHOW CREATE TABLE mongo_master.users;
SELECT * FROM mongo_master.users;


::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

zookeeper cloudera manager 


/home/cloudera/cloudera-manager --express

service hive-metastore start

 sudo service hive-server2 restart

:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::.



sqoop import -m 1 --connect jdbc:mysql://quickstart:3306/retail_db --username=retail_dba --password=cloudera --warehouse-dir=/user/hive/warehouse/ --table categories --where "order_id>1" --compression-codec=snappy --as-parquetfile --hive-import























