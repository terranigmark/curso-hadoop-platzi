## Administrar un cluster de hadoop 

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

```bash
zookeeper cloudera manager 
```

```bash
/home/cloudera/cloudera-manager --express
```



```bash
service hive-metastore start
```

```bash
sudo service hive-server2 restart
```

