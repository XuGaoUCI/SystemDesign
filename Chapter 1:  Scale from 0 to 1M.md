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

Relational database (MySQL, Oracle, PostgreSQL)
- Store data in rows and tables
- Perform join 
- long hisotry and mostly used 
- ~1K QPS not scalable compared to non-relational DB

Non-relational database
- stores: key-value, graph, column, document

