---
layout: post
title: The tail at scale
tags: [papers]

---

**The Tale at Scale** published by Google shows great advices about how to handle latency variability for large distributed system.

 For intearactive service, it's a big challenge to keep the tail latency short as the whole system scales up from both of size and complexity. 

> Just as fault-tolerant computing aims to create a reliable whole out of less-reliable parts, large online services need to create a predictably responsive whole out of less-predictable parts; we refer to such systems as “latency tail-tolerant,” or simply “tail-tolerant.”

This paper introduces approaches from 2 aspects: reducing variation; living with variation

### Reduce Variation###

* _Differentiating service classes and higher-level queuing_
* _Reducing head-of-line blocking_. break long-running requests into a sequence of smaller requests to allow interleaving of the execution of other short-running requests.
* _Managing background activities and synchronized disruption_.

### Live with Variation###

If variation can't be avoided, live with it. Goolge didn't try to solve all of the things together, but develop tail-tolerant techniques that mask or work around temporary latency pathologies.

#### Within Request Short-Term Adaptations

* **Hedged requests** to send same request to multiple replicas(a common strategy in a broad class of web services), and use the first arrived results from whichever replica. Why it names as "**Hedged requests**" is that client should send the request to the most approriate replica firstly, and will send second request to another replica after a short brief delay. Once the client receives the response, it will cancel remaining requests.
* **Tied requests**  A weakness exists for Hedged requests, which is that in some time window, multiple servers will execute the same requests.  This problem can be capped by set the delay as 95% expected latency, but it will limits the benefits to a small portion. A common source of variability is before the request begins execution, it has to be queueing in server. **Tied requests** can solve this: enqueuing copies of a request in multiple servers simultaneously and allowing the servers to communicate updates on the status of these copies to each other. When a request starts execution, a cancel request will be sent to counterpart.

#### Cross-Request long-term Adaptations #### 

* **Micro-partitions**    generate many more partitions than there are machines in the service, then do dynamic assignment and load balancing of these partitions to particular machines.
* **Selective replication**  detect or even predict certain items that are likely to cause load imbalance and create additional replicas of these items.
* **Latency-induced probation**  By observing the latency distribution of responses from the various machines in
  the system, intermediate servers sometimes detect situations where the system performs better by excluding a particularly slow machine, or putting it on probation.

