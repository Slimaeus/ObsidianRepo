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
# 3️⃣API Gateway
---
## 📈Motivation
---
### 🧩Consequences of Splitting a Service
- The single API now split into *multiple APIs*
- So now we need to:
	- Update the frontend code to be aware of the internal organization of our system
	- Make calls to different services on the browser depending on the taks
## 🏷Definition, Benefits and Quality Attributes
---
#### ❓Definition
- The API Gateway follows a software architecture pattern called *API composition*
- We compose all the APIs of all our services into one single API
- The client applications can call one single service
#### 🎁Benefits
1. Seamless internal modifications/Refactoring
2. Consolidating all security, authorization and authentication in a single place
3. Request Routing
	- We save the overhead of authentication every request from the user at each service by performing it in a single place
	- We can also save the user from making multiple requests to the different services
4. Static content and response caching
5. Monitoring and Alerting
6. Protocol Translation
## ❗ Considerations and Anti-Patterns
---
1. API Gateway shouldn't contain any business logic
	- The main purpose of an API Gateway is:
		- API composition
		- Routing requests to different services
	- Following the anti-pattern of adding business logic to our API Gateway will make it too smart
	- We may end up again with a single service that:
		- Does all the work
		- Contains an unmanageable amount of code
	- This was the problem we wanted to solve initially by splitting our system into *multiple services*
2. API Gateway may become a Single Point of Failure
	- We can solve: Scalability, Availability, Performance by deploying multiple instances of API Gateway and placing them all behind an *load balancer*
	- Our entire system becomes unavailable to the client if:
		- We push a bad release
		- Introduce a bug that may crush the API Gateway
	#### ❓What to do to avoid a Single Point of Failure
	- Eliminate any possibility of human error
	- Deploy new releases to the API Gateway with caution
3. Avoid bypassing API Gateway from external services