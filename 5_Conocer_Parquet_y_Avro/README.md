# Check data in SQL 

```bash
cd dbs_hadoop
docker-compose up 
docker inspect mysql_db
```

```bash
mysql --host=ip --user=db_username --password=db_pw -P 3306 db_name
```

```bash
show tables; 
```

```bash
select * from user_details limit 4; 
```

```bash
mysql --host=ip --user=root --password=rootpwd -e "select * from db_name.user_details" -B > user_data.tsv

```
```bash
docker run \
	--hostname=quickstart.cloudera \
	--privileged=true \
	-it \
	-v $PWD:/src \
	--publish-all=true  \
	-p 8888:8888  \
	-p 8080:80  \
	-p 7180:7180  \
	cloudera/quickstart  \
	/usr/bin/docker-quickstart 
```

```bash

gzip user_data.tsv 

```

```bash
hdfs dfs -mkdir /user/cloudera/raw_data/
hdfs dfs -put *.gz /user/cloudera/raw_data/
```

```bash
hdfs dfs -ls /user/cloudera/raw_data
```




