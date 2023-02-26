# 1️⃣Performance
---

# 2️⃣Scalability
## 1. Vertical Scalability
- Definition: Adding resources or upgrading the existing resources on a single computer
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
- Definition: Adding more resources in a form of new instances running on different machines
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

# 3️⃣Availability
---
1. Definition: The fraction of thime / probability that our service is operationally functinal and accessible to the user.
2. Formula of Availability
	- Uptime = Time that our system is operationally functinal and accessible to the user
	- Downtime = Time that oru system is unavailable to the user
	- Availability (in %) = Uptime / (Entire time our system is running)

<div style="border-style:solid; text-align:center">Availability = Update / (Uptime + Downtime) </div>

1. Alternative way to Calculate / Estimae Availability
	- MTBF - Mean Time Between Failures
	- MTTR - Mean Time to Recovery

<div style="border-style:solid; text-align:center">Availability = MTBF / (MTBF + MTTR) </div>


