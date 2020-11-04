usando sqoop 



sqoop import-all-tables  -m 1  --connect jdbc:mysql://localhost:3306/db_name  --username=db_username  --password=db_pw  --compression-codec=snappy  --as-parquetfile  --warehouse-dir=/user/cloudera/platzo  --hive-database platzi --hive-overwrite --hive-import







 docker run --hostname=quickstart.cloudera --privileged=true -it -v $PWD:/src --publish-all=true -p 8888:8888 -p 8080:80 -p 7180:7180 cloudera/quickstart /usr/bin/docker-quickstart
 

sqoop import -m 1 --connect jdbc:mysql://quickstart:3306/retail_db --username=retail_dba --password=cloudera --warehouse-dir=/user/hive/warehouse/ --table customers --compression-codec=snappy --as-parquetfile --hive-import

invalidate metadata;
show tables;
select * from customers;







mysql --host=172.24.0.2 --user=db_username --password=db_pw -P 3306 db_name


sqoop import-all-tables \
-m 1 \
--connect jdbc:mysql://quickstart:3306/retail_db \
--username=retail_dba \ --password=cloudera \
--compression-codec=snappy \
--as-parquetfile \
--warehouse-dir=/user/hive/warehouse \
--hive-overwrite
--hive-import

mysql --host=ip --user=db_username --password=db_pw -P 3306 db_name
show tables; 

select * from user_details limit 4; 


sqoop import --query 'SELECT a.*, b.* FROM a JOIN b on (a.id == b.id) WHERE $CONDITIONS' --split-by a.id --target-dir /user/foo/joinresults




sqoop list-tables --connect jdbc:mysql://172.25.0.3:3306/db_name  --username root  --password root_pwd



sqoop import-all-tables -m 1 --connect jdbc:mysql://172.25.0.3:3306/db_name --username=db_username --password=db_pw --compression-codec=snappy --as-parquetfile --warehouse-dir=/user/hive/warehouse --hive-overwrite --hive-import




sqoop import-all-tables -m 1 --connect jdbc:mysql://172.25.0.3:3306/db_name --username=db_username \--password=db_pw --compression-codec=snappy --as-parquetfile --warehouse-dir=/user/hive/warehouse --hive-overwrite --hive-import




