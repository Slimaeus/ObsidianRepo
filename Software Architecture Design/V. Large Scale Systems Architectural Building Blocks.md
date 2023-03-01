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
# 2️⃣Message Broker
---
## 💪Motivation
---
### ❌Synchronous Communication - Drawbacks
1. Both application instances have to remain healthy and maintain this connectin to complete the transaction
2. No padding in the system to absorb a sudden increase in trafic or load
### ✔Message Broker
1. Remain Healthy and Maintain Connectino
	- It's easy to achieve this when two services exchange small messages that take short time to process and respond
	- It can get complex when a service takes a long time to complete its operation and provide a response
## 📈Benefits and Capabilities
---
### 📔Introduce
- A software architecural block that uses  the <u>queue data structure to store messages</u> between senders and receivers
- A message broker is used *inside* our system and not exposed externally
### 📦Capabilities
- Basic capabilities:
	- Storing/temporarily buffering the messages
	- Message routing
	- Transformation validation
	- Load balancing
- Loose Coupling between Senders and Receivers
	- Entirely *decouple* senders fom the receivers
	- The fundamental building block of **asynchronous** software architecture
### 📈Benefits
- Most message broker implemetations offer the *publish/subscribe pattern* where multiple services can:
	- Publish messages to particular channel
	- Subscribe to that channel
	- Get notified when a new event is published
## ❕Quality Attributes
---
### 😣Fault Tolerance
- A message broker adds a lot of fault tolerance to our system
- It allows different services to communicate with each other while some of them may be unavailable temporarily
- Message brokers prevent messages from being lost
### 🆙Availability and Scalability
- The additional fault tolerance helps us provide high availability to our users
- A message broker can queue up messages when there is a traffic spike
- It allows our system to scale to high traffic
### 🎩Performance
- We pay a little in performance when it comes to latency
- A message broker adds significant indirection between two services
- This performance penalty is not too significant for most systems