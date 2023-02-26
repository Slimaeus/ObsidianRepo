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

# 4️⃣Fault Tolerence & High Availability
1. Sources of Failure
	1. Human Error
		- Pushing a faulty config to production
		- Running the wrong command / script
		- Deploying an incompletely tested new version of software
	2. Software Errors
		- Long garbage collections
		- Out-of-memory exceptions
		- Null pointer exceptions
		- Segmentation faults
	3. Hardware Failures
		- Server / routers / storage devices breaking down due to limited shelf-life
		- Power outages due to natural disasters
		- Network failures because of:
			- Infrastructure issues
			- General congesion
2. Methods of Achieving High Availability & Fault Tolerence
	1. Introduction to Fault Tolerence
		- Failures will happen despite:
			- Improvements to our code
			- Review testing, and release processes
			- Performing ongoing maintenance to our hardware
		- <u>Fault Tolerance</u> is the best way to achieve <u>High Availability</u> in our system
	2. Definition
		- *"Fault Tolerance enables our sytem to remain operational and available to the users <u>despite</u>failures within one or multiple of its componets "*
	3. Fault Tolerance
			- When failures happen a falut-tolerant system will:
				- Continue operating at the same / reduced level of performance
				- Prevent the system from becoming unavailable
	4. Tactics for achieving Fault Tolerance: Fault Tolerance revolves around 3 major tactics:
		- Failure Prevention
		- Failure Detection and Isolation
		- Recovery
		1. Failure Prevetion
			- To prevent our entire system from going down, eliminate any <u>Single Point of Failure</u> in our system
			- Examples of a Single Point of Failure can be:
				- One server where we're running our application
				- Storing all our data on the one instance of our database that runs on a single computer
			- Best way to eliminate a single point of failure is through <u>Replication and Redundancy</u>
			- Types of Redundancy
				- Spatial Redundancy - Running replicas of our application on different computers
				- Time Redundancy - Repeating the same operation / request multiple times until we succeed / give up
			- Strategies for Redundancy and Replication
				- Two strategies which are extensively used in the industry in different systems:
					- Active-Active architecture
						- Advantages
							- Load is spread among all the replicas
							- Identical to horizontal scalability
							- Allows more traffic
							- Better performance
						- Disadvantages
							- All the replicas are taking requests
							- Additional coordination required to keep active replicas in sync
					- Active-Passive architecture
						- Advantages
							- Implementation is easier
							- There is a clear leader with up-to-date data
							- Rest of the replicas are followers
						- Disadvantages
							- Ability to scale our system is host
							- All the request still go to only one
		2. Failure Detection
			1. False Positive
				- But the issue might be <u>the network</u> or <u>long garbage collection</u>
				- Then the monitoring service is going to have a **false positive**
				- It assumed that a healthy host is faulty
			2. False Negative
				- The Monitoring Service shouldn't have **false negatives**
				- False negatives mean that:
					- The servers may have crased
					- The monitoring system did not detect that
			3. Monitoring System Functions
				- Exchange of messages in the form of pings and heartbeats
				- Collect data about the number of errors each host gets per minute
					- If the error rate in one of the hosts is hight, it can interpret that as <u>failure of the host</u>
				- Collect information about time taken for each host to respond
					- If the time to respond to requests becomes long, it can decide that the <u>host is slow</u>
		3. Recovery from Failure
			- Actions after detecting faulty instance / server:
				- Stop sending traffic /workload to that host
				- Restart the host to make the problem go away
				- Rollback - going back to a version that was stable and correct
					- Common in databases
					- If we get to a state violating some condition / data, we can <u>roll back to the last correct state</u> in the past
					- If we detect errors while rolling out new versions of software, we can <u>roll back to the previous version</u>

# 5️⃣SLA, SLO, SLI
1. SLA - Service Level Agreement
	- It is a legal contract that represents our quality services such as:
		- Availability
		- Performance
		- Data durability
		- Time to respond to system failures
	- It states the penalties and financial consequences, if we breach the contract
	- The penalties include:
		- Full / Partial refunds
		- Subscription / License extensions
		- Service credits
	- SLAs exist for:
		- External paying users (always)
		- Free external users (sometimes)
		- Internal users within our company (occasionally)
	- Internal SLAs don't include any penalties
		- SLA for free external users makes sense if our system has major issues during a free trial of our service
		- We compensate those users with a <u>trial extension</u> or <u>credits for future</u>
		- Companies providing entirely free services don't publish SLA
2. SLOs - Service Level Objectives
	- Individual goals set for our system
	- Each SLO represents a <u>target value / range</u> that our service needs to meet
	- SLOs include:
		- Quality attributes from the beginning of the design process
		- Other objectives of our system
3. SLIs - Service Level Indicators
	- Quantitative measure of our compliance with a service-level objective
	- It is the actual numbers:
		- Measured using a monitoring service
		- Calculated from our logs
	- It can be later compared to our SLOs
4. Important Considerations
	1. We shouldn't take every SLI that we can measure in our system and define an objective associated with it
	2. Promising fewer SLOs is better
	3. Set realistic goals with a budget for error
	4. Create a recovery plan for when the SLIs show that we are not meeting our SLOs

