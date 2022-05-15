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

