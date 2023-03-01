# 1️⃣Introduce
1. What is an API?
	- That interface is a contract between:
		- <u>Engineers</u> who implement the system
		- <u>Client applications</u> who use the system
	- Since this interface is called by other applications, it is referred to as an **Application Programming Interface** or **API**
	- In a large-scale system, API is called by other applications remotely through the network
	- The applications calling our API may be:
		- <u>Frontend clients</u> like mobile applications / web browers
		- <u>Backend systems</u> that belong to other companies
		- <u>Internal systems</u> within our organization
	- Each component of our system will have its own API
	- The component API's will be called by other applications within our system
2. API categories
	1. Public APIs
		- Exposed to the general public
		- Any developer can use / call them from their application
		- Good practice:
			- Required the users to register with us before allowing to send requests and use the system
		- This allows:
			- Control over who uses the system externally
			- Control over how they use the system
			- Better security
			- To blacklist users breaking rules
	2. Private APIs
		- Exposed only internally within the  company
		- They allow other teams / parts of the organization to:
			- Take advantage of the system
			- Provide bigger value for the company
			- Not expose the system directly outside the organization
	3. Partner APIs
		- Similar to Public APIs
		- Exposed only to companies / users having business relationship with us
		- The business relationship is in the form of:
			- Customer Agreement after buying our product
			- Subscribing to our service
3. Benefits of a well designed API
	1. Client who uses it can immediately and easily <u>enhance thier business</u> by using our system
	2. They need not know anything about our system's internal design / implementation
	3. Once we define and expose our API, <u>clients can integrate with us</u> without waiting for full implementation of our system
	4. API makes it easier to design and architect the internal structure of our system
		- It defines the endpoints to the different routes that the user can take to use our system
		- 
4. API best practices and patterns
	1. Complete Encapsulation
		- Complete Encapsulation of the internal design and implementation
		- Abstracting it away from a developer wanting to use our system
		- If client wanting to use our API:
			- Requires any information about how it is implemented internally
			- Nedds to know our business logic to use it
		- Then, the whole purpose of the API is defeated
		- API should be completely decoupled from our internal design and implementation
		- We can change the design later without breaking the contract with our clients
		- 
	2. Easy to use
		- Easy to <u>use</u>
		- Easy to <u>understand</u>
		- Impossible to <u>misuse</u>
		- The ways to make an API simple can be:
			- Only <u>one way</u> to get certain data / perform a task
			- <u>Descriptive names</u> for actions and resources
			- Exposing <u>only the information</u> and actions that users need
			- Keeping things <u>consistent</u> all across our API
	3. Keeping the Operations Idempotent
		- "An operation does't have any additional effect on the result if it is performed more than once"
		- Updating the user's address to a new address is an Idempotent Operation
		- The result is the same regardless of performing it any number of times
		- Idempotent Operations are preferred for our API as they are going to be used through the network
		- If the client application sends us a message:
			- The message can be lost
			- The response to that message may be lost
			- The message wasn't received as a critical component in our system went down
		- Because of network decoupling, the client application has no idea which scenario actually happened
		- If our operation is idempotent, they can simply resend the same message again without any consequences
	4. API Pagination
		- Important when a response from our system to the client request contains a very large payload or dataset
		- Without pagination most client 
			- Not be able to handle big responses
			- Result in a poor user experience
		- Imagine what would happen if:
			- After opening your email account, you see all the emails you ever received instead of the latest emails
			- After searching for an item on online store / serach engine, you see too many items that matched your query
		- The client application / web browser is unlikely to handle so much data
		- It would take an unreasonable time to show all those results
		- Pagination allows the client:
			- To request only a small segment of the response
			- Specify the mximun size of each response from our system
			- Specify an offset within the overall dataset
		- To receive the next segment we increment the offset
	5. Asynchronous Operations
		- Some operations need one big result at the end
		- Nothing meaningful can be provided before the entire operation finishes
		- If the operation takes a long tiem, the client applications has to wait for the result
		- The pattern used for these situations is an <u>Asynchronous API</u>
		- A client application *receives a response immediately* without having to wait for the final result
		- That response includes some kind of identifier that allows:
			- To track the progress and status of the operation
			- Receive the final result
	6. Versioning our API
		- Best API design allows us to make *changes to the internal design and implementation* without changing the API
		- In practice, we may need to make n*on-backward compatible API changes*
		- If we explicitly version the APIs we can:
			- Maintain two versions of the API at the same time
			- Deprecate the older one gradually

# 2️⃣RPC
---
## 1. How RPC works
- Unique Features of RPC
	- The remote method invocation looks like calling a normal local method in terms of the developer code
	- This is referred to as <u>location transparency</u>
	- To the developer of the client application a method executed *locally* or *remotely* looks the same
	- RPC frameworks support *multiple* programming languages
	- Applications writter in different programming languages can talk to each other using RPC
- RPC Over Time
	- This concept of implementing an API using an RPC has been around for decades
	- The only thing that changes over time are:
		- The frameworks
		- The details of their implementation
		- Thier efficiency
	- Our job as API developers is:
		- To pick an appropriate framework
		- Define the API and the relevant data types using IDL
		- Publish that description
## 2. Benefits of RPC
- Convenience to the developers of the client applications
- They can communicate with our system easily by *calling methods on objects* similar to calling *normal, local methods*
- The details of *communication establishment* or *data transfer between client to server* are abstracted away from the developers
- Failures in communication with server result in an *error* or *exception* depending on the programming language
## 3. Drawbacks of RPC
- Unlike local methods executed on the client-side, remote methods are:
	- Slower
		- The client never knows how long those remote method invocations can take
		- Slowness can be addressed by introducing <u>asynchronous versions</u> for slow methods
	- Less reliable
		- The client is remotely running on a computer and is using the network to communicate with our system
		- Carelessness in designing the API can introduce confusing situations for the client application developers
- There is no real way for the client to know whether:
	- The server *received* the message and the *acknowledgement message got lost* in the network
	- The server *crushed* and *never received* the message
- To solve the unreliability problem, we can stick to the best practice of <u>making our operations idempotent</u> when possible
## 4. When to user RPC
- RPC are used in communication between two backend systems
- Frameworks that support RPC from frontend clients are less common
- RPC is a perfect choice for:
	- API provided to a different company instead of an end user app/web page
	- Communication between different components within a large system
	- Abstracting away the network communication and focusing only on the actions the client wants to perform
- RPC approach would not be a good fit:
	- Where we don't want to abstract the netwrok communication away
	- When we want to take direct advantage of HTTP cookies or headers
- RPC revolves more around actions and less around data/resources
- In RPC, every action is a new method with a different name and signature
- We can define many methods/actions without limitation
- Other styles of APIs can be a better fit when:
	- Designing an API that is more data-centric
	- All the operations need are simple CRUD (Create, Read, Update, Delete) operations