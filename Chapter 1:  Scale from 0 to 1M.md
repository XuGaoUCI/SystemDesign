# Chapter 1 Scale from zero to millions of users
## Single server setup
A single server request flow is illustrated as below.

![single server](https://github.com/XuGaoUCI/SystemDesign/blob/main/images/chap1_simple_request_flow.PNG)

Highlights:
- DNS is a paid service by 3rd parties and not hosted by our servers.
- IP address is returned to browser or mobile app.
- After IP is obtained, HTTP requests are sent to web server.
- The web server returns HTML pages / JSON for rendering.

Traffic sources:
- Web application
server-side (Java / Python etc.)
client-side (HTML / Javascript)
- Mobile application
HTTP is a communication protocol between web and mobile server. JSON is popular for API to transfer data.
## Database
![with database](https://github.com/XuGaoUCI/SystemDesign/blob/main/images/chap1_simple_request_db.PNG)
Relational vs non-relational database

Relational database (MySQL, Oracle, PostgreSQL etc.)
- Store data in rows and tables
- Perform join 
- long hisotry and mostly used 
- ~1K QPS not scalable compared to non-relational DB

Non-relational database (Cassandra, Hbase, MongoDB, Mamcached, Redis etc.)
- stores: key-value, graph, column, document
- Join might not be supported? (I would rather say efficiently join is hard)
- low latency
- data is unstructured 
- massive amout of data 
- high QPS 10 QPS (MongoDB, Cassandra) 100K - 1M QPS (Redis, Memcached)

Vertical Scaling vs Horizontal Scaling

Vertical Scaling (scale up)
- Add CPU / RAM etc.
- Fit for low traffic 
- Simple
- Has hard limit 
- No failover / redundancy / replica

Horizontal Scaling (scale out)
- Large scale application
- Add more servers etc.
- Many users
- Reliability / Available 

## Load Balancer
![with lb](https://github.com/XuGaoUCI/SystemDesign/blob/main/images/chap_simple_lb.PNG)

Highlights:
- Clients connect to public IP of load balancer and can not communicate directly with servers
- Private IPs used for communication between servers with the same network
- Failover issue / availability 
  - Serve 1 down, traffic routed to server 2 while adding a new healthy server
  - Traffic grows rapidly, add new servers and LB will send requests to new ones

## Database replication
![with db replica](https://github.com/XuGaoUCI/SystemDesign/blob/main/images/chap1_simple_db_replica.PNG)

Highlights:
- Performance: Write goes to master while read goes to slave. It allows parallel processed queries 
- Availability: Website remains online if one database server is down
  - Only one slave database. If it goes down, read request will be directed to master temporarily. A new slave will be replacing the old one. 
  - Multiple slave databases. One goes down, read request will be routed to other replicas and replacement is done.
  - If master database goes down, one slave will be promoted to new master. A new slave will replace the old one. In practice, promoting is difficult as slave database might not have the most updated data. One needs to backfill data. Multi-master / circular replication might help.
- Reliability: If one database server is destroyed, data won't be lost b/c it has replications

## Reflection Point
So far, we have a basic design 
- Users gets IP address of LB from DNS
- Users interacts with LB with this IP address
- Request is routed to server through LB
- A web server reads data from a slave database
- A web server routes write / update/ insert/ delete etc. data-modifying requests to master database.

Next, we consider improve the load / response time.

