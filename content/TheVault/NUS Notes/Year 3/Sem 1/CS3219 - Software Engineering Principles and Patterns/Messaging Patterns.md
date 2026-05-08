---
title: Messaging Patterns
Date Created: 2025-11-20
Last Updated: 2025-11-20
tags:
  - CS3219
  - SWE/Communication/Messages
---
# Communication
---
In general in a <b><span style='color: #B0E0E6'>distributed application development</span></b> (*DAD*), when we think about communication it can be between components or applications.

For **components** it can be as simple as an direct API call or [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Event Driven Architecture.md#Events|events]] or [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Communication.md#Event vs Message|messages]].

For **applications** (*docker and Kubernetes*) it it through a file, database or even through RPC or Rest API calls.

>[!failure] Challenges in communication between application / components
>- Different platforms, programming languages & data formats
>- Needs a common understanding between applications / components
>- Network unreliability
>- Deal with changes in the application / component  protocol

So to get things to **communicate through a distributed setting** (*through the network on different servers, entirely different applications*), is by using a <b><span style='color: #B0E0E6'>message oriented middleware</span></b> (*MOM*) or a messaging broker.

>[!example] An example of a message broker or MOM is Java Message Service (JMS)
>Other more industry standard API and protocols are Amazon MQ

MOM <b><span style='color: #F0E68C'>takes care of seamless communication</span></b> and since we are using a middleware, then we are making things <b><span style='color: #98FB98'>loosely coupled</span></b>.

>[!quote] Every DAD needs a MOM
# Enterprise Integration
---
So what technologies are there to allow 2 separate applications to talk to one another?

There are **3 scenarios** when thinking about enterprise integration:
1) **Point to point**: There is a <b><span style='color: #F0E68C'>communication pathway to all services</span></b>, making it <b><span style='color: var(--mk-color-red)'>tightly coupled</span></b>
2) **Hub-spoke integration**: We have a <b><span style='color: #F0E68C'>hub which acts like a mediator</span></b> and forwards the communication request using spokes based on user specification (*API gateway*). However there is a <b><span style='color: var(--mk-color-red)'>single point of failure on the hub</span></b>. But it is alright for small scale applications.
3) **Enterprise service bus** (*ESB*): It is a <b><span style='color: #F0E68C'>message based abstraction</span></b> (*must use the message mechanism*). Unlike hub & spoke it <b><span style='color: #F0E68C'>just sends or reads the message to the middleware</span></b>. The rest is done by the middleware (*like where to forward to*).

So we want to use technology to <b><span style='color: #F0E68C'>tightly connect everything</span></b> in an enterprise landscape.

>[!info] Goal of enterprise integration
>To <b><span style='color: #F0E68C'>seamlessly share information</span></b> with each other.
>
>This is why messaging is important.

So **enterprise integration patterns** are <b><span style='color: #F0E68C'>technology-independent</span></b> solutions to common integration problems (*like our singleton pattern it just tells you how it should be done but not explicitly what to use*).
# Message Patterns
---
![[List of Messaging Systems.png|center]]

There are many messaging systems to:
- Construct messages
- Transport messages
- Route messages to proper destination
- Transform messages to a required format
- Produce & consume messages
- Manage & test the system

So **every MOM or message broker** should <b><span style='color: #F0E68C'>support these capabilities</span></b>.
## Message Construction

A [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Communication.md#Event vs Message|message]] is a encapsulated <b><span style='color: #F0E68C'>method requests & data structures</span></b> sent across the network

It is made up of 3 things:
1) **Header**: Which specifies the metadata of the message like information type, origin, destination, size, id etc
2) **Properties**: This <b><span style='color: #F0E68C'>more user defined </span></b> for example in RabbitMQ there is name, auto delete, time to live etc
3) **Body**: Which is your data (*payload*), it can be <b><span style='color: #B0E0E6'>command</span></b> (*expects a return*), <b><span style='color: #B0E0E6'>document</span></b> (*intendent recipient*), <b><span style='color: #B0E0E6'>event</span></b> (*broadcasted*)
## Message Channels

It acts as a medium, to <b><span style='color: #F0E68C'>get messages from 1 point to another</span></b> (*point to point*).

>[!note] When we talk about channel it is the same as a queue
><b><span style='color: #F0E68C'>Channel is a patten</span></b>, the queue is like a implementation. But they are both the same thing.

A channel <b><span style='color: #F0E68C'>transmits messages in one direction</span></b>. So if we want a **2 way message it needs 2 separate channel**, one for request the other for reply.

So the <b><span style='color: #B0E0E6'>requestor</span></b> is the one who <b><span style='color: #F0E68C'>sends the request message</span></b> and wait for a reply. The message can be **sent** even if the <b><span style='color: var(--mk-color-red)'>replier is not running</span></b>. Thus the <b><span style='color: #F0E68C'>message must be persisted</span></b>.

The <b><span style='color: #B0E0E6'>replier</span></b> is the one who receives the message and <b><span style='color: #F0E68C'>replies with a message</span></b>. Here the receiver will get a <b><span style='color: #B0E0E6'>receive request</span></b> and will send a reply message after it is done.

>[!example] Request / reply message in JMS
> A **sent request** (*request message*) will look like:
> ```json
> {
> 	time : 10000,
> 	message_id : 123
> 	correlation_id: null
> 	reply_to : reply_queue //where to send the reply to
> 	contents: hello world //Payload
> }
> ```
> A **receive request** will look like:
> ```json
> {
> 	time : 10100,
> 	message_id : 123
> 	correlation_id: null
> 	reply_to : reply_queue //where to send the reply to
> 	contents: hello world
> }
> ```
> A **reply** will look like:
> ```json
> {
> 	time : 10200,
> 	message_id : 124
> 	correlation_id: 123 // This reply is related to the message sent (id)
> 	reply_to : null
> 	contents: hello world // Response
> }
> ```

So notice that in the message it will have a <b><span style='color: #B0E0E6'>return address</span></b>, it tells the replier <b><span style='color: #F0E68C'>where to send the reply to</span></b>. Each of these channels has a unique identifier (*like a IP address*).

>[!question] What if there are many requestors sending to the same request channel?
>Then the message will <b><span style='color: #F0E68C'>contain the recipient of the reply</span></b>.
>
>Which is essentially the unique identifier of the reply channel.

There is also a <b><span style='color: #B0E0E6'>corelation id</span></b>, which <b><span style='color: #F0E68C'>maps the response to which request is it responding to</span></b>. This allows the sender to know when it gets a reply, which request is this reply for.

So the corelation id consist of:
- Requestor
- Replier
- Request (*The actual request itself*)
- Reply
- Request ID
- Correlation ID

>[!success] With the corelation id we can have a audit trail
>It is useful if we want to have a trail from the chain of requests for <b><span style='color: #F0E68C'>audit purposes</span></b>.
### Special Cases

So what if the **message cannot be processed?** Then it will be placed into a <b><span style='color: #B0E0E6'>invalid message channel</span></b>. This channel <b><span style='color: #F0E68C'>handles erroneous messages</span></b> and is used as an audit.

There is also something called a <b><span style='color: #B0E0E6'>dead letter channel</span></b>, this is to <b><span style='color: #F0E68C'>handle messages that cannot be delivered</span></b> (*network issues, processing issues*).

>[!info] This is where the time to live in the message properties comes in
>So after the time to live, it expires and will be moved to the dead letter channel. Which afterward will triggers some actions to do (*maybe try and fix the message or send a notification*).

There is also a <b><span style='color: #B0E0E6'>data type channel</span></b> which basically <b><span style='color: #F0E68C'>separates the messages by data type</span></b> (*[[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Communication.md#RabbitMQ|RabbitMQ]]*). So our <b><span style='color: #F0E68C'>receivers will do something based on data type</span></b> regardless what the message is about. 

The sender will need to know what data type it is sending and send it to the correct channel.
### Publish-Subscribe Channel

Also known as <b><span style='color: #B0E0E6'>pub-sub</span></b>. It is used when <b><span style='color: #F0E68C'>multiple parties are interested in certain messages</span></b>. So in a sense it is broadcasted to all interested parties.
#### One-way

The channel just sends the message and <b><span style='color: #F0E68C'>does not require a response</span></b>.

The receiver can also add a **filter** (*[[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Messaging Patterns.md#Message Filter|message filter pattern]]*) to <b><span style='color: #F0E68C'>filter out unwanted messages</span></b>.

>[!example] Examples of a 1 way pub sub is Google Cloud PubSub & Amazon MQ
#### Request-Response

In some cases you need to <b><span style='color: #F0E68C'>aggregate all their responses</span></b> before moving forward. So a response queue is used.

>[!question] What if we only want 1 response instead of all responses?
>Then we can <b><span style='color: #F0E68C'>employ a filter</span></b> to filter out only 1 response.
>
>The rest can go to the [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Messaging Patterns.md#Special Cases|dead letter channel]].

>[!note] A pub-sub is used for request messages but a p2p channel is used for response messages

>[!example] Examples of a request-response pub sub is Amazon MQ
## Message Routing

The purpose of a message router is to <b><span style='color: #F0E68C'>get the message to the right person</span></b>. It has some logic or <b><span style='color: #F0E68C'>conditions</span></b> which they will <b><span style='color: #F0E68C'>consume the message and reinsert them</span></b> into the correct message channel(s).

So recall that in a message there is a **recipient inside the metadata**, this means that the <b><span style='color: var(--mk-color-red)'>sender needs to determine where it is being sent to</span></b>.

To <b><span style='color: #98FB98'>reduce the workload</span></b> of the sender, it will just send the data to the router and the router will take care of where to send this to.

There are 2 types of routers:
1) **Simple** routers which <b><span style='color: #F0E68C'>routes messages</span></b> from one inbound channel to one or more outbound channels
2) **Composed** routers <b><span style='color: #F0E68C'>combines multiple simple routers</span></b> to form a complex message flow

>[!important] If we are sending to more than 1 recipient we need a way to replicate the message
>We can either have a mechanism to <b><span style='color: #F0E68C'>duplicate the message</span></b>.
>
>Or we can use a <b><span style='color: #B0E0E6'>splitter</span></b> and a <b><span style='color: #B0E0E6'>aggregator</span></b>.
>
>A [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Messaging Patterns.md#Message Splitter|splitter]] <b><span style='color: #F0E68C'>splits the message into smaller parts</span></b> and the [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Messaging Patterns.md#Message Aggregator|aggregator]] <b><span style='color: #F0E68C'>combines all the smaller responses</span></b> into the original response.
### Content-Based Router

This type of routers <b><span style='color: #F0E68C'>examines the message content</span></b> and routes it based on the content.

>[!question] What does it mean by content based?
>Assuming in the message there is a credit card information details, so when the router sees this it will know it is for payment, so it will route it to there.

So the **router** should <b><span style='color: #F0E68C'>know all possible recipients</span></b> and their capabilities / datatypes.

So **any new recipient** will <b><span style='color: var(--mk-color-red)'>require a change</span></b> in the content based router. However it <b><span style='color: #98FB98'>decouples between the sender & receiver</span></b>.

>[!failure] Could be hard to manage the router
>The router needs to know the participants and adding & removing will need to update this router.
#### Message Filter

It is a **special kind of content based router**, that <b><span style='color: #F0E68C'>eliminates undesired messages</span></b>.

>[!important] This filter has a single output channel
>So it has a regular **input channel**, where <b><span style='color: #F0E68C'>all the broadcasted messages comes</span></b> in. Then only the <b><span style='color: #F0E68C'>approved ones</span></b> will be sent to the **output channel**.

>[!question] So use message filter or content based?
>It depends, if you have <b><span style='color: #F0E68C'>a lot of filter conditions</span></b>, it might be better to **use the message filter**. If not then the <b><span style='color: var(--mk-color-red)'>workload is heavy on the router itself</span></b>.

It is <b><span style='color: #F0E68C'>usually used with pub-sub channels</span></b>. So the <b><span style='color: #F0E68C'>management of the message lies with the filter</span></b>.
### Context-Based Router

This router decides on the destination based on <b><span style='color: #F0E68C'>specific contexts</span></b>.  It is commonly used for:
- Load balancing
- Testing
- Failover functionality

>[!example] An example on how context-based router works
>So if a component fails, the router will send the message to another component.
>
>Or like in [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Software Engineering Principles & Patterns.md#Continuous Deployment Strategies|blue-green deployment]], if the context is blue then it will be sent to the blue environment.
### Message Splitter

It <b><span style='color: #F0E68C'>splits a single message into multiple smaller segments</span></b>. Then we will use a content based router

>[!important] This is not a router
>A splitter is <b><span style='color: #F0E68C'>used along side</span></b> a [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Messaging Patterns.md#Content-Based Router|content based router]] to router the different smaller segments.

>[!note] Each smaller segment will have the same corelation ID
>This is to ensure that the recipient who aggregates them know all of them is for the same message.

>[!example] An example on how a message splitter can work
>For example if an order arrives. It can be split based on vendor to be sent to the different vendor services to check inventory and so on.
### Message Aggregator

Usually used along side the splitter to <b><span style='color: #F0E68C'>aggregate the messages into 1 single message </span></b>.

>[!question] How does it know which messages to aggregate?
>It <b><span style='color: #F0E68C'>uses the corelation ID</span></b> to know which ones to combine.
### Message scatter-gather

Essentially it <b><span style='color: #F0E68C'>broadcasts a message</span></b> to a number of participants concurrently and then <b><span style='color: #F0E68C'>aggregate all their replies</span></b> into 1 single message.

It is ideal for requesting responses from multiple parties then aggregating and processing the data

>[!example] Example on a scatter-gather usage
>Lets say you want to find all prices for this particular item in all vendors. So you can broadcast to find the price to each vendor.
>
>Then use a aggregator to aggregate everything and its gives a list of prices.
## Message Transformation

<b><span style='color: var(--mk-color-red)'>Different application uses different data formats</span></b>. So this is where the <b><span style='color: #B0E0E6'>translator</span></b> comes in. It encapsulates message format transformation to allow messages to be <b><span style='color: #F0E68C'>converted to the correct type</span></b>.

>[!example] An example of a translator is EDI 850

These translators allows applications to <b><span style='color: #98FB98'>not need to know each other data formats</span></b>.

>[!warning] However with a large number of applications we might need 1  translator for each pair
>
>This is known as <b><span style='color: #B0E0E6'>point to point mappings</span></b>. And this is not good as it is <b><span style='color: var(--mk-color-red)'>hard to manage</span></b> (*A change in the data format results in a chain of changes in the translator*).
>
>Then if we have a **new application** we need to <b><span style='color: var(--mk-color-red)'>add more translators</span></b>.

By standard it is better to use <b><span style='color: #B0E0E6'>canonical mappings</span></b>. It is like an interface for the datatype or a <b><span style='color: #F0E68C'>common data type structure</span></b> (*canonical data model or CDM*).

>[!failure] It can be expensive to convert to a canonical mapping

Afterwards the **recipient** of the message will take the translated message and <b><span style='color: #F0E68C'>untranslated it back to their own data format</span></b>.

>[!example] An example is Unix which uses files as a canonical data

So the sender can translate into the canonical format or have a translator do it for you.
## Message Endpoint

This is how the application <b><span style='color: #F0E68C'>connects to the messaging system</span></b> so it can send and receive messages.

This is essentially our **messaging API** which acts as an <b><span style='color: #F0E68C'>interface</span></b> between the application & messaging system.

>[!tldr] This messaging endpoint is customised
>This endpoint is <b><span style='color: #F0E68C'>customised</span></b> based on the application and the messaging system client's API.
>
>The rest of the application will not know any details about this (*message format, channels, etc*).

>[!important] An endpoint can only send or receive but never both

These <b><span style='color: #F0E68C'>endpoints are channel specific</span></b>, meaning that different channels will have their own endpoint.

>[!note] We can also control the rate in which it consumes messages
>This is known as throttling the message consumption
### Types of Message Consumer Endpoints

#### Polling Consumer

The receiver can be a polling consumer which <b><span style='color: #F0E68C'>proactively reads messages</span></b> (*receiver is constantly looking for messages*) when it is ready to consume them.

It is like constantly poll the broker for a message.

>[!example] An example of this is [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Communication.md#RabbitMQ|RabbitMQ]] `basic.get` function

>[!failure] It uses a lot of CUP cycles
#### Event-driven consumer

The receiver can be a event-driven consumer which <b><span style='color: #F0E68C'>reactively reads messages</span></b>.

The receiver will inform the broker it is ready to consume a message. When the broker sends a event to the receiver then it will do something

>[!example] An example of this is [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Communication.md#RabbitMQ|RabbitMQ]] `basic.consume` function