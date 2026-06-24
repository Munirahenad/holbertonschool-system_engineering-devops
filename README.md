Web Infrastructure Design

This project contains web infrastructure diagrams and explanations for hosting the website www.foobar.com.

The goal of this project is to understand how a web infrastructure grows from a simple single-server setup into a distributed, secured, monitored, and scalable architecture.

Tasks Overview

0. Simple Web Stack

This task represents a basic one-server web infrastructure.

Main components:

* 1 domain name: foobar.com
* www.foobar.com DNS record pointing to 8.8.8.8
* 1 server
* 1 web server: Nginx
* 1 application server
* 1 set of application files / code base
* 1 MySQL database

Purpose:

This design explains the basic flow of a user accessing a website.
The user requests www.foobar.com, DNS resolves the domain to the server IP address, and the server handles the request using Nginx, the application server, the code base, and MySQL.

Main issues:

* Single Point of Failure (SPOF)
* Downtime during maintenance
* Limited scalability when traffic increases

⸻

1. Distributed Web Infrastructure

This task improves the first design by adding a load balancer and two backend servers.

Main components:

* 1 HAProxy load balancer
* 2 backend servers
* Each backend server contains:
    * Nginx web server
    * Application server
    * Application files / code base
    * MySQL database
* MySQL Primary-Replica replication

Purpose:

This design distributes traffic between two servers using HAProxy.
The load balancer uses a Round Robin algorithm, which sends requests to each server one by one.

This setup is Active-Active because both backend servers are online and receiving traffic.

Main issues:

* The single HAProxy load balancer is still a SPOF
* The Primary MySQL database can be a SPOF if there is no automatic failover
* No firewall
* No HTTPS
* No monitoring

⸻

2. Secured and Monitored Web Infrastructure

This task adds security and monitoring to the distributed infrastructure.

Main components:

* 3 firewalls
* 1 SSL certificate to serve www.foobar.com over HTTPS
* 3 monitoring clients
* HAProxy load balancer
* 2 backend servers
* MySQL Primary-Replica replication
* Monitoring service such as Sumologic

Purpose:

This design secures the infrastructure by adding firewalls and HTTPS.
The SSL certificate allows encrypted traffic between the user and the website.

Monitoring clients are installed on the servers to collect logs, metrics, and health data.
This data is sent to a monitoring platform such as Sumologic.

Main issues:

* SSL termination at the load balancer can be an issue if internal traffic is not encrypted
* Only one MySQL server accepts write operations
* Having web server, application server, and database components together can cause resource competition

⸻

3. Scale Up

This task improves scalability by adding another server, adding a second load balancer, and separating the main components.

Main components:

* 2 HAProxy load balancers configured as a cluster
* Dedicated web server
* Dedicated application server
* Dedicated database server
* Separated web, application, and database layers

Purpose:

This design separates the infrastructure into different layers.
The web server handles web traffic, the application server handles backend logic, and the database server stores and retrieves data.

Adding a second HAProxy load balancer creates a load balancer cluster, which improves availability and reduces the load balancer as a single point of failure.

Main benefits:

* Better scalability
* Better resource isolation
* Easier maintenance
* Improved availability
* Clear separation between web, application, and database layers

Technologies Used

* Web Server: Nginx
* Application Server: Generic application server
* Database: MySQL
* Load Balancer: HAProxy
* Security: Firewall, SSL/TLS, HTTPS
* Monitoring: Sumologic or similar monitoring service
* DNS: Domain name resolution for www.foobar.com

Learning Objectives

By completing this project, I learned how to:

* Explain the role of each component in a web infrastructure
* Understand how DNS connects a domain name to a server IP address
* Explain the difference between a web server and an application server
* Understand how a load balancer distributes traffic
* Explain Active-Active and Active-Passive setups
* Understand Primary-Replica database replication
* Identify Single Points of Failure
* Explain why HTTPS and firewalls are important
* Understand how monitoring collects logs and metrics
* Explain how separating components improves scalability and maintenance
