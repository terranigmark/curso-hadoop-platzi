
# Bases de datos con Hadoop importando datos con sqoop y manejo de datos con Hive

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
sqoop import-all-tables \
    -m 1 \
    --connect jdbc:mysql://quickstart:3306/retail_db \
    --username=retail_dba \
    --password=cloudera \
    --compression-codec=snappy \
    --as-parquetfile \
    --warehouse-dir=/user/hive/warehouse \
    --hive-import
```

```bash
hadoop fs -ls /user/hive/warehouse/
hadoop fs -ls /user/hive/warehouse/categories/

```


```bash
invalidate metadata;

show tables;

```


```bash
-- Categorias mas populares
select c.category_name, count(order_item_quantity) as count
from order_items oi
inner join products p on oi.order_item_product_id = p.product_id
inner join categories c on c.category_id = p.product_category_id
group by c.category_name
order by count desc
limit 10;

```
