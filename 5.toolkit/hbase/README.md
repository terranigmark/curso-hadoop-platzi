hbase shell 
list 
create 'newtbl', 'knowledge'
list 

describe 'newtbl'
status 'summary'
put 'newtbl','r1','knowledge:books','Alicia en el pais de las maravillas'
put 'newtbl','r1','knowledge:books','Alicia a través del espejo'
put 'newtbl','r2','knowledge:books','Odisea'
put 'newtbl','r2','knowledge:books','Iliada'


scan 'newtbl'
