[[RDS]] [[Database]] 

The goal The following are the goals of this hands-on: 
1. Create a MySQL RDS fully managed instance 
2. Run sample queries (only for technical learners) 
3. Understand the simplicity of database management on the cloud

## Hands on
RDS has its own AWS Console | interface - same as any other service 

### Creation Method
Standard - you manage all settings 

Easy Create - AWS selects the settings based on best practices

### Engine Selection
There are multiple engines available - MySQL, Maria SQL, Oracle etc. 
- you also choose the engine's version

![[Pasted image 20250731173752.png]]

For this TIO we selected Dev/Test template, which is not as fast as the Production but provides a good environment for testing. 

Also for *Availability and Durability* we only created 1 primary instance, but here you can choose how much redundancy you want

### Credential Settings
You choose the master username - in this case root and you can also choose if you want to use AWS password manager to store the credentials or you manage it yourself. In this case we chose: *Self Managed* 

### Instance Configuration
In this section there are a lot of settings, some I want to note is the *Storage Autoscaling* you can let the instance auto scale if its capacities are exceeded

You can also determine how much storage and what type of instance - db.t2.micro or db.t2.mciro ... etc 

There also a section for *burstable classes* -> this allows a short-term burst of performance above baseline (cpu, network or memory) 

### Additional Settings
Here you can find the check box for *Backups* as well for *encryption* and *auto minor version upgrade* <- these settings should be toggled for production.


--- 
After enabling/disabling these settings we created the DB instance. It can take a bit to start

Then we created a basic EC2 instance that allowed us to SSH into the DB instance via this command:
```shell
mysql -h RDS_ENDPOINT -u root -p
```

RDS_ENDPOINT:
gl-rds.c2nnpahz9s69.us-east-1.rds.amazonaws.com

from here we can use MySQL

### Using Python Code to Interact With RDB
```python
import mysql.connector

  

db_host = 'gl-rds.c2nnpahz9s69.us-east-1.rds.amazonaws.com'

db_username = 'root'

db_password = 'password'

database = 'employees'

  

# Simple routine to run a query on a database and print the results:

def doQuery(conn) :

cur = conn.cursor()

#cur.execute("SELECT [TBD: place any of the employees table columns] FROM employees limit 10")

#for [TBD: provide any variables here to be accessed by PY seperated by comma] in cur.fetchall() :

# print [TBD: use the same PY variables here seperated by comma]

cur.execute("SELECT emp_no, first_name, last_name, email_id FROM employees limit 10")

for emp, firstname, lastname, email in cur.fetchall() :

print(emp, firstname, lastname, email)

  
  

def mysqlConnector() :

print("\n\nUsing mysql.connector")

print("---------------------")

conn = mysql.connector.connect(host=db_host, user=db_username, passwd=db_password, db=database)

doQuery(conn)

conn.close()

  
  

def createOrder() :

print ("\n\nCreating new record in the orders table")

conn = mysql.connector.connect(host=db_host, user=db_username, passwd=db_password, db=database)

cur = conn.cursor()

# TBD:You have to write this code and submit as part of the lab

create_order_sql = (

"insert into orders ("

" OrderID, OrderUserID, OrderAmount, OrderShipName, OrderShipAddress, OrderShipAddress2,"

" OrderCity, OrderState, OrderZip, OrderCountry, OrderPhone, OrderFax, OrderShipping,"

" OrderTax, OrderEmail"

") values (%s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s, %s)"

)

order_data = (

'ord00111', 16528, 125.50, 'Starfleet Academy', '1225 Audelia drive', '#1971',

'Fort Baker', 'California', '560102', 'USA', '+91 12345 67890', '+91 55689 66541', 0,

10.75, 'kirk@starfleet.com'

)

cur.execute(create_order_sql, order_data)

  

conn.commit()

cur.close()

conn.close()

  
  

def main() :

mysqlConnector()

# Create a sample order record in the order table. This will be used by the advanced version

createOrder()

  
  

main()
```


### Using elasticache
```python
|   |
|---|
|#*********************************************************************************************************************|
|# Author - Nirmallya Mukherjee|
|# This script will connect to a MySQL DB using multiple driver options & use Redis cache for optimization|
|# Pre-requisite is the rds.py exercise|
|#|
|# Create a Elasticache Redis cluster|
|# Configure and create new cluster radio|
|# Cluster mode disabled|
|# Name = mycache|
|# Location = AWS Cloud|
|# Disable Multi-AZ and Aito-failover|
|# Node type = cache.t2.micro|
|# Replicas = 0|
|# Create new subnet group; Name = mycache-subnetgroup; VPC = should be the default VPC (same as RDS as well as EC2)|
|# Security: select default-sg|
|# Disable auto backups, Minor version upgrades|
|#|
|# Need to install redis module as follows|
|# sudo pip3 install redis|
|# To check the keys in redis (if redis is running in a docker container) use ->|
|# redis-cli keys '*'|
|#*********************************************************************************************************************|
||
|import mysql.connector|
|import redis|
|import pickle|
||
|#Example elasticache end point can be redis.scsdmx.ng.0001.usw2.cache.amazonaws.com|
|db_host = 'REPLACE WITH RDS DNS here'|
|redis_host = 'REPLACE WITH Elasticache primary endpoint DNS here'|
||
|db_username = 'root'|
|db_password = 'password'|
|database = 'employees'|
||
||
|class Order:|
|def __init__(self, orderid, userid, shipping, email):|
|self.orderid = orderid|
|self.userid = userid|
|self.shipping = shipping|
|self.email =email|
|self.tostring()|
|def tostring(self):|
|#print(" Order is {0} {1} {2} {3}").format(self.orderid, self.userid, self.shipping, self.email)|
|print (" Order is %r %r %r %r" % (self.orderid, self.userid, self.shipping, self.email))|
||
||
|def getAllOrders() :|
|print ("\n\nUsing mysql.connector")|
|print ("---------------------")|
|conn = mysql.connector.connect(host=db_host, user=db_username, passwd=db_password, db=database)|
|cur = conn.cursor()|
|cur.execute("SELECT OrderID, OrderUserID, OrderShipName, OrderEmail FROM orders")|
|for orderid, userid, shipping, email in cur.fetchall() :|
|order_obj = Order(orderid, userid, shipping, email)|
|cur.close()|
|conn.close()|
||
||
|def getOrder(order_id):|
|print ("\nGetting the order", order_id)|
|red = redis.StrictRedis(host=redis_host, port=6379, db=0)|
|red_obj = red.get(order_id)|
|if red_obj != None:|
|print ("Object found in cache, not looking in DB")|
|#Deserialize the object coming from Redis|
|order_obj = pickle.loads(red_obj)|
|order_obj.tostring()|
|else:|
|print ("No key found in redis, going to database to take a look")|
|conn = mysql.connector.connect(host=db_host, user=db_username, passwd=db_password, db=database)|
|cur = conn.cursor()|
|cur.execute("SELECT OrderID, OrderUserID, OrderShipName, OrderEmail FROM orders where OrderID='%s'" % (order_id))|
|for orderid, userid, shipping, email in cur :|
|order_obj = Order(orderid, userid, shipping, email)|
|#Serialize the object|
|ser_obj = pickle.dumps(order_obj)|
|red.set(order_id, ser_obj)|
|print (" Order fetched from DB and pushed to redis")|
|cur.close()|
|conn.close()|
||
||
|def main() :|
|getAllOrders()|
|getOrder('ord00111')|
||
||
|main()|
||
```

