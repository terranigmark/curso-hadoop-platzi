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

mysql -uroot --password=rootpwd -h 172.23.0.2 -P 3306









mongoexport --host 172.25.0.3 --db hadoop --collection elements --type csv --fields=first_name,gender  --out names.csv

mysql -h 172.25.0.2 -u root --password=rootpwd -e "select * from db_name.user_details" -B > user_data.tsv
