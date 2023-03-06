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

# 4️⃣CAP Theorem
---

# 5️⃣Scalable Unstructured Data Storage