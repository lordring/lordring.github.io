---
layout: post
title: Reactive Microservices
---

Notes of [Reactive Microservice Architecture](http://www.oreilly.com/programming/free/reactive-microservices-architecture-orm.csp).

## Principles ##

* Isolate All the Things

>  Any organization that designs a system (defined broadly) will pro‐duce a design whose structure is a copy of the organization’s com‐munication structure. 

* Act Autonomously

* Do One Thing, and Do it Well

  * Unix philosophy
  * SRP

* Own Your State, Exclusively

  > Microservice take sole responsibility for their own state and the persistence thereof. Modeling each service as a Bounded Context can be helpful since each service usually defines its own domain, each with its own Ubiquitous Language. Both these techniques are taken from the Domain-Driven Design (DDD) toolkit of modeling tools. 

  * Event Sourcing and CQRS

* Embrace Asynchronous Message-Passing

* Stay Mobile, but Addressable

### Microservices Come in Systems ###

* Service Discovery 

  * [Service Registery](http://microservices.io/patterns/service-registry.html) & [Client Side Service Discovery](http://microservices.io/patterns/client-side-discovery.html)
  * Server-Side Service Discovery
  * It is often better to rely on distributed AP-based9 Peer-to-Peer technologies that use techniques like Epidemic Gossip sometimes together with Conflict-Free Replicated Data Types (CRDTs) to disseminate the information in a simpler, eventually consistent and resilient way—without the need for additional infrastructure
    * Examples of AP-based service discovery systems include Lightbend Reactive Platform,Netflix Eureka, Serf, and regular DNS

* API Management

  * Robustness Principle: be conservative in what you do, be liberal in what you accept from others
  * API gateway: receiving requests from the client, routing it to the right set of services

* Managing Communicative Patterns

  * Scalable MQ
    * Publish-Subscribe: Kafka, Amazon Kinesis
  * Customise

* Integration

  * [Reactive Streams](http://www.reactive-streams.org/) specification (Reactive Streams-compatible products include Akka Streams, RxJava, Spark Streaming, and Cassandra drivers)
  * Faulty services management: retry tasks; Circuit Breaker Pattern(Netflix Hystrix, Akka)
  * Event Streaming Platforms for system integration from [Fast Data](https://info.lightbend.com/rs/558-NCX-702/images/COLL-white-paper-fast-data-big-data-evolved.pdf)

* Minimizing Data Coupling 

  * minimize the service-to-service coordination of state


  * [comfortably share silence](https://speakerdeck.com/pbailis/silence-is-golden-coordination-avoiding-systems-design)
  * Minimizing the Cost of Coordination	


  ​	