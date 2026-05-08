---
title: Communication
Date Created: 2025-11-19
Last Updated: 2025-11-19
tags:
  - CS3219
  - SWE/Communication
---
# Synchronous & Asynchronous Communication
---
As [[Year 3/Sem 1/CS3219 - Software Engineering Principles and Patterns/Microservices.md#Service Communication|briefly mentioned previously]], there is **synchronous** communication which sends a request and waits for a response (*request-reply pattern*).

>[!fail] Issues with synchronous communication
>- Tightly coupled
>- Connection overhead (*needs to maintain the connection*)
>- Sender handles failures (*connection drop, timeout, what if we cannot hold the connection for a long period, etc*)

There is also **asynchronous** communication where the sender sends a request and does something else. This enables <b><span style='color: #F0E68C'>independent functioning of sender & receiver</span></b>. This makes it <b><span style='color: #98FB98'>loosely coupled</span></b>.

>[!fail] Issues with synchronous communication
>- Need notification mechanism, how does the receiver returns a response
>- Sender has to map response to the request being sent (*multiple requests sent*)

>[!tldr] Request reply patten but Asynchronous
>We can <b><span style='color: #F0E68C'>use the return as a notification mechanism</span></b>.
>
>Basically the receiver can send a response 202 saying request received and sends some link (*some end point*) to check the progress.
>
>Then the client can just use this link to get the result when it is completed (*response 302*).

We <b><span style='color: #F0E68C'>can have both async and synchronous communication used</span></b> in the same architecture / application.
# Event vs Message
---
**Both** of them are <b><span style='color: #F0E68C'>constructs</span></b>, they both <b><span style='color: #F0E68C'>utilise asynchronous communication</span></b>, they also <b><span style='color: #F0E68C'>facilitate decoupling of services</span></b> (*both uses a middleware*) and also <b><span style='color: #F0E68C'>carry information</span></b> (*payload*) for the other one to consume.

>[!important] The difference is the intent in which they are sent

A **event**, the data is sent to a broker / topic where <b><span style='color: #F0E68C'>consumers can subscribe to receive it</span></b> (*broadcasted, pub-sub*).

>[!example] Kafka is a event broker

>[!info] The publisher owns the event
>Since it <b><span style='color: #F0E68C'>knows that a event happens</span></b> and thus sends the relevant payload. It also knows which topic to publish the event to which topic.

A **message**, the data is sent to a <b><span style='color: #F0E68C'>queue & there is a designated recipient on the other end</span></b> (*point to point*), which <b><span style='color: #F0E68C'>must be executed</span></b>.

>[!important] Sender only guarantee that message is sent (*Reliable delivery*)
>No guarantee on when or if the message is read and process by receiver (*receiver can be down forever*).

>[!info] The receiver owns the message
>When sending a request, it is to change the current state. So the recipient will own the message since it <b><span style='color: #F0E68C'>defines how to request and how data should be sent to accept the request</span></b>.

>[!example] AWS SQS is a message broker

These messages can be a:
- **Command**: To perform some action
- **Query**: To get some data

>[!question] When do we use message or event
>It depends, if there is <b><span style='color: #F0E68C'>a lot of services</span></b> then maybe use an **event**.
>
>It it is like <b><span style='color: #F0E68C'>a few services</span></b> then consider a **message** as events are more expensive for smaller systems and are easier to implement (*Just a API call*).
## Topic vs Queue

A **topic** is a <b><span style='color: #F0E68C'>one to many communication</span></b>. So a sender sends something and it can reach multiple subscribers simultaneously.

It <b><span style='color: #F0E68C'>allows for non-sequential processing</span></b>. Remember that each event will have a unique offset. With <b><span style='color: #F0E68C'>multiple partitions, there can be a difference between the order</span></b> in which the events are processed.

A **queue** only has <b><span style='color: #F0E68C'>a single designated receiver</span></b>.

The queue follows a first in first our principle, so <b><span style='color: #F0E68C'>whichever message arrives first will be the first to be processed</span></b>.

>[!question] Why do we need the queue?
>Since we are doing **asynchronous communication**, the <b><span style='color: #F0E68C'>queue acts as a buffer</span></b>, so you do not need to wait.
>
>It also <b><span style='color: #98FB98'>enables persistent communication</span></b>, as the queue holds the message until it is consumed.
# Single Vs Multiple Receivers
---
So as mentioned previously, **single receivers** are just <b><span style='color: #F0E68C'>point to point</span></b> communication (*unicasting*). So the message queue used acts like a buffer and messages are <b><span style='color: var(--mk-color-red)'>never copied to other receivers</span></b>.

**Multiple receivers** are more of a <b><span style='color: #F0E68C'>pub/sub</span></b> mechanisms. They can also be <b><span style='color: #F0E68C'>published into a topic</span></b>, so listeners can subscribe to the topic they are interested in.
## Kafka

A popular **pub/sub system** used is <b><span style='color: #87CEEB'>Kafka</span></b>, which is open source. A Kafka <b><span style='color: #F0E68C'>cluster contains multiple brokers</span></b> (*just servers*) and **each broker** <b><span style='color: #F0E68C'>hosts a topic which can contain partitions</span></b> (*topics has a identifier*).

By **allowing to add multiple brokers** leads to <b><span style='color: #98FB98'>horizontal scaling</span></b>. And they can communicate between one another.

>[!question] Why do we need partitions?
>It allows multiple writes essentially to the same topic to <b><span style='color: #98FB98'>improve performance and speed</span></b>.
## Advance Message Queue Protocol

<b><span style='color: #B0E0E6'>AMQP</span></b> is an asynchronous communication protocol which is a <b><span style='color: #B0E0E6'>peer-to-peer protocol</span></b>.

it is an open standard and it allows conforming <b><span style='color: #F0E68C'>client applications to communicate with</span></b> conforming <b><span style='color: #F0E68C'>messaging middleware brokers</span></b>.

>[!info] Peer to peer protocol
> Peer to peer means that the sender and a broker is 1 peer and the receiver and the broker is the other pair.
> 
> Or you can think about it as the sender and receiver is 1 peer and communication if facilitated by a broker.

**AMQP example**:
![[AMPQ Example.png|center]]

Recall that the message is own by the receiver/consumer. So it dictates the format of the data. So AMQP simplifies this by <b><span style='color: #F0E68C'>allowing the publisher to send data in whatever format or not knowing what API call to use</span></b>.

>[!note] There can be more than 1 broker which talk to each other to get the message accross

The **exchange** is the component that does the heavy lifting by <b><span style='color: #F0E68C'>routing the messages to specific queues</span></b>.

>[!question] How does routing work?
> There is a set of <b><span style='color: #F0E68C'>binding rules which determines which queue</span></b> the message goes to depending on the queue's <b><span style='color: #B0E0E6'>binding key</span></b>.

Then everything else is the same, the broker can send deliver the message or the consumer requests the messages.
### RabbitMQ

It is one example which uses the AMQP protocol. So similarly, a producer will send a message to an exchange and then based on the <b><span style='color: #B0E0E6'>message attributes</span></b> (*routing key*) will <b><span style='color: #F0E68C'>route to the corresponding queue</span></b>.

>[!info] Routing Key
>It is <b><span style='color: #F0E68C'>a message attribute</span></b>, which tells which queue to go to. Usually it is just the name of the queue.

RabbitMQ's <b><span style='color: #F0E68C'>queue is persistent</span></b>, meaning that the message will remain until the consumer handles the message.

So how does the exchange does the routing? Well there are a few **exchange types** used:
1) **Direct**: The routing key <b><span style='color: #F0E68C'>matches exactly</span></b> with the queue name or key
2) **Fanout**: It is <b><span style='color: #B0E0E6'>multicasting</span></b> not broadcasting where the <b><span style='color: #F0E68C'>message is duplicated and set to a set of queues</span></b>.
3) **Topic**: Uses a <b><span style='color: #F0E68C'>wildcard matching</span></b>, for instance `us.#` will match with anything with `us.`
4) **Header**: <b><span style='color: #F0E68C'>Uses the headers</span></b> instead of the routing key. So if the header contains `format = zip` it will route to the queue that accepts `format = zip`
# Persistent vs Transient Communication
---
**Persistent** communication (*store-and-forward delivery*) essentially stores the message <b><span style='color: #F0E68C'>indefinitely until the message is consumed</span></b>.

**Transient** communication on the other hand is messages are <b><span style='color: #F0E68C'>stored for small periods of time</span></b>. If the message **cannot be delivered** (*not online for BOTH parties*) then it will be <b><span style='color: var(--mk-color-red)'>discarded</span></b>.
## Persistence & Synchronicity

1) **Persistent Asynchronous**
- Sender can just send the message without getting blocked
- Message may take an arbitrary amount of time to reach the receiver
- <b><span style='color: #F0E68C'>Sender may or may not be running</span></b> when the message is received by the receiver
- <b><span style='color: #F0E68C'>Disk or memory queues</span></b> can be used for **persistence**
- There is a <b><span style='color: #98FB98'>guarantee that message will eventually reach the receiver</span></b>

2) **Persistent Synchronous**
- **Blocked** <b><span style='color: #F0E68C'>until an acknowledgement</span></b> of the message being received is given
- The message stays in the receivers queue for an arbitrary amount of time

3) **Transient Asynchronous**
- Sender is not blocked
- <b><span style='color: #F0E68C'>Receiver has to be running</span></b>, <b><span style='color: var(--mk-color-red)'>if not the message is discarded</span></b>
- **Same** goes for <b><span style='color: var(--mk-color-red)'>any router in between is down</span></b>

4) **Transient Synchronous**
- There is **receipt-based**, where the sender is blocked until an <b><span style='color: #F0E68C'>acknowledgement is received</span></b>. But this <b><span style='color: var(--mk-color-red)'>does not tell us if the process has started</span></b> on the receiver end.
- There is **delivery-based**, same it gets blocked until the <b><span style='color: #F0E68C'>recipient starts the process of the message</span></b> (*delivery*). The acknowledgement is a bit later than receipt-based. It is a <b><span style='color: #F0E68C'>asynchronous RPC</span></b> (*remote procedure call*)
- Lastly there is **response-based**, it gets blocked until it <b><span style='color: #F0E68C'>receives a response</span></b>. It is a <b><span style='color: #F0E68C'>traditional RPC</span></b>, where it gets blocked for the entire duration.



