# 1️⃣Performance
---

# 2️⃣Scalability
## 1. Vertical Scalability
- Pros
	- Any application can benefit from it
	- No code changes are required
	- The migration between different machines is very easy
- Cons
	- The scope of upgrade is limited
	- We are locked to a centralized system which <u>cannot</u> provide
		- High Availability
		- Fault Tolerence
## 2. Horizontal Scalability
- Pros
	- No limit on scalability
	- It's easy to add / remove machines
	- If designed correctly we get:
		- High Availability
		- Fault Tolerence
- Cons
	- Initial code changes may be required
	- Increased complexity, coordination overhead
## 3. Team / Organization Scalabity
1. Definition: The measure of a systems ability to handle a growing amout of work, in an easy and cost effective way, by adding resources to the system
2. Reasons for Productivity Degradatios
	- Many crowded meetings
	- Code merge conflict
	- Business Complexity - Longer ramp up time
	- Testing is harder and slower
	- Releases become very risky
3. Increase Team Scalability
	1. Each team 1 module (Still lightly couple)
	2. Breakdown into multiple services (Better engineering productivity and scale up organizations)