# RabbitMQ

RabbitMQ is a message-queueing software also known as a message broker or queue manager. Simply said, it is software where queues are defined, to which applications connect in order to transfer messages. RabbitMQ is a reliable and mature messaging and streaming broker, which is easy to deploy on cloud environments, on-premises, and on your local machine.

![RabbitMQ](https://github.com/user-attachments/assets/b737f254-b191-4175-ab49-ad13df5aec16)

## RabbitMQ Example

A message broker acts as a middleman for various services (e.g., a web application, as in this example). They can be used to reduce loads and delivery times of web application servers by delegating tasks that would normally take up a lot of time or resources to a third party that has no other job.

In this guide, we follow a scenario where a web application allows users to upload information to a website. The site will handle this information, generate a PDF, and email it back to the user. Handling the information, generating the PDF, and sending the email will, in this example case, take several seconds. That is one of the reasons why a message queue will be used to perform the task.

When the user has entered information into the web interface, the web application will create a "PDF processing" message that includes all of the important information the user needs into a message and place it onto a queue defined in RabbitMQ.

### RabbitMQ Workflow Tutorial

The basic architecture of a message queue is simple - there are client applications called producers that create messages and deliver them to the broker (the message queue). Other applications, called consumers, connect to the queue and subscribe to the messages to be processed. Software may act as a producer, or consumer, or both a consumer and a producer of messages. Messages placed onto the queue are stored until the consumer retrieves them.

## When and Why Should You Use RabbitMQ?

Message queueing allows web servers to respond to requests quickly instead of being forced to perform resource-heavy procedures on the spot that may delay response time. Message queueing is also useful when you want to distribute a message to multiple consumers or to balance loads between workers.

The consumer takes a message off the queue and starts processing the PDF. At the same time, the producer is queueing up new messages. The consumer can be on a totally different server than the producer, or they can be located on the same server. The request can be created in one programming language and handled in another programming language. The point is, the two applications will only communicate through the messages they are sending to each other, which means the sender and receiver have low coupling.

![RabbitMQ Workflow](https://github.com/user-attachments/assets/fab99e8a-054e-4b76-bacb-ac8a7d0b05f9)

## Exchanges

Messages are not published directly to a queue; instead, the producer sends messages to an exchange. An exchange is responsible for routing the messages to different queues with the help of bindings and routing keys. A binding is a link between a queue and an exchange.

![Exchanges](https://github.com/user-attachments/assets/3854c862-861c-466b-a7dc-6fbcbb588d7f)

## Types of Exchanges

Part 2 of the tutorial uses direct exchanges. A deeper understanding of the different exchange types, binding keys, routing keys, and how or when you should use them can be found in Part 4: RabbitMQ for Beginners - Exchanges, Routing Keys, and Bindings.

![Exchange Types](https://github.com/user-attachments/assets/abf333c8-55aa-4255-9953-77044d3770f8)

- **Direct:** The message is routed to the queues whose binding key exactly matches the routing key of the message. For example, if the queue is bound to the exchange with the binding key `pdfprocess`, a message published to the exchange with a routing key `pdfprocess` is routed to that queue.
- **Fanout:** A fanout exchange routes messages to all of the queues bound to it.
- **Topic:** The topic exchange does a wildcard match between the routing key and the routing pattern specified in the binding.
- **Headers:** Headers exchanges use the message header attributes for routing.
