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
# 4️⃣CDN
---
## 📈Motivation
---
- A study by Google Analytics indicated: 53% of mobile users abandoned a website if it took longer than <b><u>3 seconds</u></b> to load
- We can improve our system's performance by:
	- Replicating our service
	- Running it on more data centers
- <u>But</u> our service is not what the users need closer
- The static content like: Images, HTML pages, Javascript, CSS files, Videos are what we need to get closer to the users to get them to load faster
## 🏷Definition, Benefits and Quality Attributes
---
#### ❓Definition
- Globally distributed network of servers
- Located in strategic places
- Main purpose: Speeding up the delivery of content to end-users
#### 🤔Problem
- CDNs were originally created to address the problem referred to as the "Wide World"
- It is a term describing a bad user experience caused by:
	- Slow internet connection
	- Overloaded web server
#### 😃Advantages
- CDNs provide service by <u>caching</u> our website content on their *edge servers* which are relocated at different *Points of Presence* (PoP)
- Those *edge servers* are:
	- Physically closer to the user
	- More strategically located in terms of network infrastructure
- This allows them to:
	- Transfer content much quicker to the user
#### 📃Types of Content
- CDNs can be userd to deliver:
	- Images
	- Text
	- CSS
	- Javascript files
	- Video streams (live and on-demand)
#### ✊Use Cases
- CDNs are used by *digital service companies* that interact with users through website/mobile app like:
	- E-commerce services
	- Financial institutions
	- Technology and software as a service (SaaS) companies
	- Media companies delivering video streaming/news
	- Social media
#### 👍Quality Attributes
- Performance - Faster page loads
- High availability - issues/slowness are less noticeable
- Security - Protection against *Distributed Denial of Service* attacks (DDos)
#### ➕Addtional Techniques
- CDN providers use *faster* and *more optimized* hard drives to store the cached content
- Reduce bandwidth by compressing the content delivered using algorithms like:
	- Gzip
	- Minification of javascript files
## 🤔Content Publishing Strategies
---
### 1. Pull Strategy
- We need to tell the content delivery network provider:
	- Which content we want on our website to be cached
	- How often this cache needs to be invalidated 
- It is configured by setting a Time To Live (TTL) property on each asset/type of asset
- Advantages
	- If our content doesn't change frequently we can simply push it <u>once</u> to the CDN
	- This significantly reduces:
		- The traffic to our system
		- The burden for our system to maintain high availability
	- Even if our system goes down temporarily, users will still get all the data from the CDN and won't be affected
- Drawbacks
	- We still need to maintain a general high availability of our system
	- The user will get an error if:
		- Certain assets expire on the CDN
		- Our system isn't available for the CDN to pull a new version
### 2. Push Strategy
- Some content delivery network providers support this model <u>directly</u>
- Others enable this strategy by <u>settign along TTL</u> for our assets so that the cache never expires
	- Whenever we want to publish a new version we purge the content from the cache
	- This forces the CDN to fetch that content from our servers whenever a user requests it
- Advantages
	- Lower maintenance on our part
	- No need to keep the CDN caches up to date once we configure:
		- Which assets need to be cached
		- How often the assets need to expire
	- Everything is taken care of by the CDN provider
- Drawbacks
	- The first users to use an asset that hasn't been cached yet will have a longer latency
	- CDN needs time to fetch the non-cached asset from our system