# ❓ What we will learn
---

## 1️⃣ Software Architecture - Motivation
---
- Anologies from Outside of the Software world
	1. Everything we build has structure
	2. The more we invest in building a product, the harder it is to change its structure
	3. The structure of the our system describes:
		- The intent of our product
		- The qualities of the product
- Application to Software
	1. Infinite ways to organize our code
	2. Different organizations will give us different properties
	3. The software architecture impacts:
		- Performance and scale of product
		- Ease of adding new features
		- Response to failure or security attack
	4. Cost of redesign will be significant in terms of time and money

## 2️⃣ Software Architecture - Definition
---
### 📔 Definition
- Many ways to define software architecture
- The definition we're going to use is as follow:

***The software architecture of a system is a high-level description of the software's structure, its different components, and how those components communicate with each other to fulfill the system's requirements and constraints.***

## 3️⃣ Software Architecture Definition - Explaination
---
### 🔓 Unpack the definition
- An abstraction that shows us the important components while hiding the implementation details
- Technologies or programming languages are ***not*** a part of the software architecture but a part of the implementation
- Decisions about implementation should be delayed to the very end of the design
- The components here are "black box" elements defined by their behavior and APIs
- Components come together to do what the <u>system must do</u>, which are our requirements
- The system <u>does not do what it shouldn't do</u>, which are the constraints

### 🔗 Levels of Abstraction
- Software architecture can have many different levels of abstraction:
	- Classes / Structs
	- Modules / Packages / Libraries
	- Services (processes / groups of processes)

### 👍 Advantages
- This more distributed, multiple service approach allows us to architect systems that can:
	- Handle large amounts of requests
	- Process and store very large amounts of data
	- Serve many users every day

### 📄 Large Scale Systems - Examples
- Ride-sharing
- Video-on-demand
- Social media
- Online video games
- Investment Services
- Banks

### ⚠ Importance of Design and Architecture

✅ Benefits:
- If we get the architecture right we can:
	- Go from a small startup to a multi-billion dollar company
	- Make a positive impact on millions of people
❌Risks:
- Not doing a good job at the design phase can
	- Waste months of engineering time
	- Build a system that doesn't meet our requirements
- Restructuring a system that was not architected correctly is very hard and expensive
- So the stakes here are high

## 4️⃣ Software Development Cycle
---

![[Pasted image 20230221191422.png]]

### ⚔ Challenges of Software Architecture
- We <u>cannot</u> prove Software Architecture to be either:
	- Correct
	- Optimal
- What we <u>can</u> do to guarantee success if follow:
	- Methodical Design Process
	- Architectureal Patterns
	- Best Practices


# Summary
- Got the intuition and motivation for Software Architecture
- Every software system has an architecture, which is critical for its success
- Definition: _"A high-level description of the software's structure, its different components, and how those components communicate with each other to fulfill the system's requirements and constraints."_
- Software Architecture is the <u>output</u> of the design phase and the <u>input</u> to the <b>implementation</b>