# 1️⃣Load Balancer
---
## 📔Introduction
---
### Role of Load Balancer: 
#### Balance load among a group of servers
## ❕Quality Attributes
---
---
### 1️⃣Scalability
- In a cloud environment, we can use auto-scaling policies to intelligently add/remove servers based on:
	- Requests per second
	- Network bandwidth
### 2️⃣High Availability
### 3️⃣Performace (Throughput)
- When it comes to performance, load balancers may add a little *latency*
- It is an acceptable price to pay for *increased performance* in terms of throughput 
### 4️⃣Maintainability

## 📃Types of Load Balancers
---
### 1️⃣DNS Load Balancing
1. DNS - Domain Name System
	- DNS is part of the internet infrastructure that maps human-friendly URLs to IP addresses
	- They can be used by network routers to route requests to individual computers on the web
	- DNS is the "phone book of the internet"
2. Advantages
	- Simple
	- Cheap (Comes for free by purchasing a domain name)
3. Drawbacks
	1. DNS doesn't monitor the health of our servers
	2. The balancing strategy is always just a simple round-robin
	3. The client application gets the direct IP addresses of all our servers
### 2️⃣Hardware Load Balancing
### 3️⃣Software Load Balancing
### 4️⃣Global Server Load Balancing
- Traffic Routing
	- Most GSLB can be configured to route traffic based on a *variety of strategies* and not just by physical location
	- Since they in constant communication with our data centers, they can be configured to route users based on:
		- The current traffic
		- CPU load in each data center
		- Best-estimated response time
		- Bandwidth between user and the data center