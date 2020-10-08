# Check data in Mongo 

db.adminCommand( { listDatabases: 1 } )
use hadoop
show collections
db.elements.find().pretty()
db.elements.count()



# Check data in SQL 
mysql --host=172.17.0.3 --user=db_username --password=db_pw -P 3306 db_name

mysql --host=ip --user=db_username --password=db_pw -P 3306 db_name
show tables; 

select * from user_details limit 4; 
