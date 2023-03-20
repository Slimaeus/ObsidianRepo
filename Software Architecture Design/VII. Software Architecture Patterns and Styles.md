# 1️⃣Introduction to Software Architecture Patterns & Styles
---
## 🏷What are Software Architecture Patterns
---
### 🤯Introduction
- General repeatable solutions to commonly occuring system design problems
- Common solutions to software architectural problems that involve <u>multiple components</u> that run as <u>seperate runtime units</u>
### 📖History
- Software architects have been observing how other companies in similar industries went about solving similar design problems
- They tried to learn:
	- What worked for them
	- What mistakes were made
- Those successful software architecture practices that became the Software Architectureal Patterns
## ❓Why Using Software Architectural Patterns
---
### 🎇Incentives
1.  Save valuable time and resources
	- If other companies:
		- Had very similar use cases to your problem
		- Operate on a similar scale
		- Already found an architecture and development practice that works for them
	- Then it's better to take that knowledge and use it
2. Avoid making our architecture resemble a Big Ball of Mud (Anti Pattern)
	- Many companies got into such situations due to:
		- Rapid growth
		- Lack of overarching, well-defined software architecture
	- A system that gets into this situation is very hard to:
		- Develop
		- Maintain
		- Scale
	- The way to avoid it is to stick to a well-defined software architectural pattern
3. Other engineers/software architects can follow it
	- Everyone can read about the pattern we're following
	- Understand exactly what to do and what not to do
### 📝Final Notes
- All the software architectural patterns are just guidelines
- As system evolve, certain architectural patterns may not fit us anymore
- We would need to migrate to a different architectural pattern that now fits us better
- Many companies already went through such migrations in the past so we can follow their best practices
# 2️⃣Multi-Tier Architecture
---
## 🏷Introduction
---
### 📊Multi-Tier Architecture
- **Logical seperation** - Limits the scope of responsibility on each tier
- **Physical seperation** - Allows each tier to be separately:
	- Developed
	- Upgraded
	- Scaled
### 📝Important Note
- **Multi-Tier** and **Multilayer** architecture are two different concepts
### ❌Restrictions in Multi-Tier Architecture
- Besides the benefits of the logical and physical seperation, there are few *restrictions* in this architectural pattern
## 🖇Three-Tier Architecture - Introduction
---
### 📊Three-Tier Architecture
- Most common and popular architectural pattern for *client-server, web-based services*
### 💻Presentation Tier
- The responsibility of the Presentation Tier is:
	- Display information to the user
	- Take the user's input
- Does not contain any business logic
- The code that runs in the client's browser is accessible and visible to the user
- It is an anti-pattern to include any business logic in this tier
### ⚙Application Tier
- Provides all the functionality and features
- Responsible for:
	- Processing the data that comes from the Presentation Tier
	- Applying the relevant business logic to it
### 🗞Data Tier
- Responsible for storage and persistence of *user* and *business-specific* data
## 🤔Three-Tier Architecture - Advantages & Disadvantages
---
### 📈Popularity
- Fits a large variety of use cases
- Any web-based service fits this model. Examples:
	- Online Store
	- News Website
	- Video/Audio Streaming Service
- Easy to scale horizontally to:
	- Take large traffic
	- Handle a lot of data
### 📉Drawbacks
- Three-Tier Architecture has <u>one</u> major drawback
- Monolithic structure of our logic tier
	- No business logic in the *presentation tier and data tier*
	- All our business logic is concentrated in a single codebase
	- Runs as a single runtime unit
### 👿Drawback Implications
1. High CPU and memory consumption
	- Makes our application slower and less responsive
	- May require us to start upgrading each computer we run our application on
	- Vertical scaling is expensive and limited
2. Low Development Velocity
	- Large and complex codebase is harder to:
		- Develop
		- Maintain
		- Reason about
	- More concurrent development will cause:
		- More merge conflicts
		- Highter overhead
	- We can mitigate this problem by:
		- Logically splitting application's codebase into separate modules
		- Release new versions of those modules only when the entire application is upgraded
	- Organizational scalability of the Three-Tier Architecture is limited
### 🏁Conclusions
- It is the perfect choice for companies whose codebase is:
	- Relatively small and not complex
	- Maintained by a small team of developers
- This includes:
	- Early-stage startups
	- Well-established companies
## 💬Other Multi-Tier Architectures
---
### ✌Two-Tier Architecture
- Less comman than Three-Tier Architecture but still pretty popular
- Advantages
	- Eliminateds the overhead of the Logic Tier
	- Provides a faster, more native experience to the users
	- Examples include:
		- Desktop/Moblie version of editors
			- Document
			- Image
			- Music
### 🤔Four/Five-Tier Architecture
# 3️⃣Microservices Architecture
---
## 🆚Microservices Architecture vs Monlithic Architecture
---
### 📉Monolithic Architecture - Disadvantages
- As the size and complexitiy of our codebase grow, it becomes difficult to:
	- Troubleshoot
	- Add new features
	- Build
	- Test
	- Load in IDE
- We have problems in organizational scalability because:
	- The more engineers we add to the team, the more code merge conflicts we get
	- Our meetings become larger, longer, and less productive
- Once we start seeing these problems, we should consider migrating our architecture towards *Microservices*
## 🦠What is Microservices Architecture
---
### 🏷Microservices Architecture
- Microservices Architecture organizes our business logic as a collection of loosely coupled and independently deployed services
- Each service is owned by a small team and has a narrow scope of responsibility
### 📈Advantages
#### 🤏Smaller Codebase
- Development becomes easier and faster
- Codebase loads instantaneously in our IDE
- Building and testing becomes easier and faster
- Trobleshooting/adding new features becomes easier
- New developers can become fully productive faster
#### 🎩Better Performance and Horizontal Scalability
- Instances become less CPU intensive and less memory-consuming
- Services can be scaled horizontally by adding more instances of low-end computers
#### 🏨Better Organizational Scalability
- Each service can be independently: Developed, Maintained, Deployed by a separate small team
- Leads to high throughput from the entire organization
- Each team is autonomous to decide on:
	- Programming languages
	- Frameworks
	- Technologies
	- Release schedule/process
#### 🛡Better security (Fault Isolation)
- If we have an issue in one of the services, it is easier to isolate it and mitigate the problem
## 💪Microservices - Considerations and Best Practices
---
### 🤔Considerations
#### 📦We don't get all these benefits out-of-the-box
- If we don't follow best practices we can fall into the *Big Ball of Mud*
#### 🤕Overhead and challenges
- Organizational Decoupling
	- We need to make sure that the services are logically separated such that <u>every change</u>:
		- Can happen only in one service
		- Would not involve multiple teams
### 💪Best Practices
#### 🙂Single Responsibility Principle
- Each service needs to be responsible for only one:
	- Business capability
	- Domain
	- Resource
	- Action
#### 💦Separate Database Per Service
- Data has to be split in a way that each microservice can be *completely independent*
- *Data duplication* is an expected overhead
### 📝Final Notes
- Following the best practices will allow us to succedd using Microservices
- We get all those benefits <u>despite</u> the complexitiy and overhead only when we reach a certain *complexity* and *organizational scale*
- It's best to start with the simple Monolithic approach first
- When Monolithic Architecture stops working, we should consider Microservices
# 4️⃣Event Driven Architecture
---
## 🏷Introduction
---
### 🎆Events
- Instead of :
	- Direct messages that issue commands
	- Requests that ask for data
- We have only <u>events</u>
- An event is an immutable statement of a fact or a change
- Examples
	- Fact Events
		- User cliking on a digital art
		- Item being added to a shopping cart
	- Change Events
		- Player of a video game
		- IoT device (vacuum cleaner)
### 🧩Components
- Producer
- Consumer
## 🌟Benefits
---
### 🖇Decoupling of Microservices
- We can decouple microservices effectively as:
	- Services don't need to know about each other's API
	- All messages are exchanges asynchronously
- Benefits:
	- Higher scalability
	- More services can be added to the system without any changes
### ⌛Real Time Stream Analysis
- Event-Driven Architecture allows us to:
	- Analys streams of data
	- Detect patterns
	- Act upon data in real-time
- Example:
	- Fraud Detection Service can detect suspicious activity in a user's account
## 🎉Event Sourcing Pattern
---

## 💦CQRS Pattern
---
1. Optimizing a database with high load of Read and Update operations
	- Concurrent operations to the same records or tables contend with each other making *all* operations slow
	- We can optimize a distributed database only for one type of operation at the exxpense of the other
		- Read-intensive workload - Conpromise on slower writes
		- Write-intensive workload - Compromise on performance of read operations
2. Joining multiple tables located in separate databases that belong to different microservices