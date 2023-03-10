# 1️⃣Relational Databases & ACID Transactions
---
## 📔Introduction to Relational Databases
---
### 🖼Schema
- The structure (schema) of each table is defined ahead of time
- This gives us the knowledge of each what each record must have
- Because of this, we can use a robust query language to <u>analyze</u> and <u>update</u> the table data
### 📃SQL - Structured Query Language
- The industry-standard scripting language to perform such queries is called SQL - <u>Structured Query Language</u>
- Different relational databse implementations have their own *additional features* to their version of that language
- The majority of *standard operations* are the same for all relational databases
### 🔍Example
Online Store:
- Products table
|ProductId|Name|Model Year|Company|Category|Base Price|
|-|-|-|-|-|-|
|1|Baby Bottle|2001|Johnson & Johnson|Baby Accessories|$9|
|2|Car Toy|2016|Toys"R"Us|Toys|$15|
|3|Sports Shoes|1999|Nike|Apparel|$59|
|...|...||...|||

- As customers place orders for those products, we need to store those orders in a separate table
- We want the ability to easily analyze and report on things like:
  - Which products sell the most/least at a given time frame
  - Rank companies based on performance of their products
  - Get break down of which category of products does better during certain sales/seasons
- Orders Table
|Order Id|Discount|Status|User Id|Product Id|
|-|-|-|-|-|
|15|0%|Pending|102|1|
|16|20%|Completed|1005|2|
|17|5%|Pending|15|3|
|18|0%|Completed|99|1|
|...|...|||...|

## 💹Advantages of Relational Databases
---
### 👾Ability to form complex and flexible queries
### 📈Efficient storage
### 🍃Natural structure of data of humans
### 🛡ACID transaction guarantees
- #### Atomicity
	- Each set of operations that are part of one transaction either:
		- Appear <u>all at once</u>
		- Don't <u>appear at all</u>
- #### Consistency
	1. *A* transaction that was *already commited* is seen by all **future** queries/transactions 
	2. A transaction doesn't violate any constraints that we set for our data
- #### Isolation
	- Related to *Atomicity* in the context of <u>concurrent</u> operations performed on our database
- #### Durability
	- Once a transactin is complete, its *final state* will **persist** and remain permanently inside the database

### 🔁Transaction
A transaction is a sequence of operations that for an external observer should appear as a single operation
## 📉Disadvantages of Relational Databases
---
### 💎Rigid structure enforced by table's schema
- The schema has to be *defined ahead of time* before we can use the table
- If we want to change the schema of a table by adding/removing a column, we would have some *maintenance time*
- We need to plan ahead in designing the scheme of our tables, so as to *not change* the schema very often or at all
### 🔧Hard to maintain/scale
### 🐌Slower read operations
## ✅When to choose a Relational Database
---
- Perform complex and flexible queries to analyze our data
- Guarantee ACID transactions between different entities in our database
## ❌When NOT to choose a Relational Database
---
- There isn't any inherent relationship between different records that justifies storing our data in tables
- Read performance is the most important quality that we need for providing good user experience
# 2️⃣Non-Relational Databases
---
## 📔Introduction to Non-Relational Databases
---
### 📚History
- A relatively new concept
- Became popular in the mid-2000s
- Solved the drawbacks of relational databases
### 🤝Logical Grouping
- They allow to logically group a set of recourds *without* forcing all of them to have the same strucutre
- We can easily add additional attributes to one/multiple records *without* affecting the already existing records
### 🔳Support Native Data Structure
- Don't store data in tables
- Support more native data structures to programming languages
- This eliminates the need for an ORM (Object Relational Mapping)
### Efficient Storage🆚Fast Queries
- Relational Databases: designed for <u>effecient storage</u>
- Non-Relational Databases: designed for <u>faster queries</u>
### 🔁Trade-offs
- When we allow *flexible schemas* we lose the ability to easily analyze those records
- Analyzing multiple groups of records (join operations) also becomes hard
- ACID transactions are rarely supported by non-relational databases
## 📃Categories of Non-Relational Databases
---
### 🔑Key/Value Store
- Key/Value store can be seen as a large-scale *hashtable* or *dictionary*
- It has very few constraints on the type of values we have for each key
### 📄Document Store
- We can store collections of documents, with more structure inside each document
- Each document is an object with different attributes
- Those attributes can be of different types
- Documents inside a document store are easily mapped to objects inside a programming language
### 📊Graph Database
- Extension of a document store with additional capabilities to: Link, Traverse, Analyze multiple records more efficiently
- Optimized for navigating and analyzing relationships between different records
- Use Cases
	- Fraud detection:
		- Multiple logical users identified as same person trying to initiate multiple transactions using same email/computer
	- Recommendation engines:
		- Recommend new products to users based on past purchase history or friends of the user 
## ✅When to choose a Non-Relational Database
---
- Analyze our use case
- Figure out which properties of a database are:
	- Most important
	- Can be compromised
- Non-relational databases:
	- Superior when it comes to query speed
	- Perfect choice for caching
- Handling real-time big data
- Data is not structed
- Different records can contain different attributes
# 3️⃣Techniques to Improve Performance, Availability & Scalability of Databases
---
## 🔢Database Indexing
---
- Speed up retrieval operations
- Locate the desired records in a sub linear time
- Without indexing, those operations may:
	- Require a "full table scan"
	- Take a long time for large tables
🎩Full Table Scan - Pefromance
- Those operations if performed *very frequently* or *on large tables* can:
	- Become a performance bottleneck
	- Impact our user's experience
### 📔Definition
`A database index is a helper table, created from a particular column/group of columns`
### 🔲Data Structures
- Once the index table is created we can put it inside a data structure like:
	- Hashmap
	- Self-balanced tree (B-Tree)
### 🖇Composite Index
- Indexes can be formed not only from *one column* but from a *set of columns*
### 🔁Indexing Tradeoffs
- **Read queries** are faster in the expanse of:
	- Additional space for storing the index tables
	- Speed of write operations
 - Note on Other Types of Databases
	 - Indexing is also used extensively in Non-Relational Databases such as document stores
## ➕Database Replication
---
### 🔁Tradeoffs
- Higher complexity when it comes to operations like:
	- Write
	- Update
	- Delete
- Is is not a trivial task to make sure that concurrent modifications to the same records:
	- Don't conflict which each other
	- Provide guarantees in terms of consistency and correctness
### ✨Distributed Database
- Difficult to design, configure and manage on a high scale
- Require competency in the field of distributed systems
### 🤝Support
- Database replication is supported by all modern databases
	- Non-Relational Databases: Incorporate replication out-of-the-box
	- Relational Databases: Support varies among different implementations
## ⚙Database Partitioning/Sharding
---
### 📈Advantages
- We can scale our database to store more data
- Different queries can be performed completely in <u>parallel</u>
- We get both:
	- Better Performance
	- Higher Scalability
### 🔁Drawback
- Database sharding turns our database into a distributed database
### ❎Non-Relational Databases
- First-class feature in all Non-Relational Databases because:
	- Records are decoupled from each other
	- Storing the records on different computers is more natural and easier to implement
### ✅Relational Databases
- In Relational Databases, the support for partitioning depends on the implementation
- Queries involving multiple records are common - Spreading them across multiple machines is challenging to implement
- When choosing a Relational Database for a use case involving high volume of data, make sure that partitioning is well supported
### 🏗Infrastructure Partitioning
Partitioning is not only used for databases but can also be used to *logically split our infrastructure*
### 📝Final Notes
- Indexing, Replication and Partitioning are completely orthogonal to each other
- We don't need to choose one over the other
- All three of them are commonly used together in most real-life large-scale systems
# 4️⃣CAP Theorem
---
## ❓Intuition
---
"In the presence of a Network Partition, a distributed database cannot guarantee both Consistency and Availability and has to choose <u>only one</u> of them."

### 👉Choices
- Forces our database to a choice <u>only</u> when there is a *network partition*
- Majority of the tiem we can easily provide *both* consistency and availability when:
	- There is no network partition
	- Our replicas can freely communicate with each other
### 📔Definitions and Terminology
---
### 🏷Terminology
#### C = Consistency
"Every read request receives either the most recent write or an error"
- A Consistent Database will return the value of the record that corresponds to the *most recent write operation*
- All clients see the same value at the same time regardless of which instance of the database they talk to
#### A = Availability
"Every request receives a non-error response, without the guarantee that it contains the most recent write"
- Different clients may get different versions of a particular record
- All requests return successfully with a *valid value*
#### P = Partition Tolerance
"The system continues to operate despite an arbitrary number of messages being lost or delayed by the network between different computers"
### 🎩Interpretation and Considerations
### 🤯Interpretations
- CAP Theorem tells us that when we either choose or configure a database we have to <u>drop one</u> of those three properties:
	- CA - no Partition Tolerance
	- CP - no Consistency
	- AP - no Availability
#### ⏺Centralized Database
- With a Centralized Database we can avoid network partitions
- But with a high amount of *data* and *query volume*, it cannot scale
- If we do choose to go the *distributed* route, we have to also choose Partition Tolerance
- Thus, we have to choose to either drop Availability or Consistency
# 5️⃣Scalable Unstructured Data Storage
---
## ❎Unstructured Data
---
- Data that doesn't follow a particular structure, schema, or model
### 🌌Where to Store Unstructured Data?
- Some databases allow storing *blobs* (Binary large object)
- Relational/non-relational databases are <u><i>not optimized</i></u> for unstructured data
- Databases have size limits on binary objects (~megabytes)
## 🤏Use cases
---
### 👤Upload User Data
### 📥Backup and Archiving
### 🕸Web Hosting
### 🤖Machine Learning and Big Data Analytics
### 🛠Main Features
- Data sets are very big
- Each file/object is very big
## ⚙Distributed File System (DFS)
---
### 📈Benefits
- No need for a speacial API
- We can modify files easily
	- Examples:
		- Modify a document
		- Append to the end of a log/video file
- Very efficient and high performance IO operations
### 🛑Limitations
- Number of files is limited
- No easy access through web API (HTTP + REST)
## 🏪Object Store / Blob Store
---
### 📈Benefits
- Scalable storage solution for storing unstructured data at internet scale
	- <u><b>Linear scalability</b></u>
- <u><b>No limit</b></u> to the number of objects we can store
- Very <u><b>high limit</b></u> on a single object size (~ 5 - 10 Terabytes)
- Provides an HTTP + <u><b>REST API</b></u> 
- Supports for <u><b>Versioning</b></u> out of the box
### ⚙More Options
- Sometimes <u>cloud-based</u> Object Stores are not an option because of:
	- **Budget** constraints
	- **Legal** constraints
	- **Performance** constraints
- We can run <u>On-Premise</u> Object Store using:
	- **Open Source** Object Stores
	- **Third-party** managed solutions
### 📉Drawbacks
- Objects are immutable
	- We can only replace an existing object with a new version
	- Has negative performance implications
- No easy file system-like access
	- Access through an SDK or REST API
- Lower IO performance comparing to a Distributed File System