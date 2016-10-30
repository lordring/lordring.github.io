---
layout: post
title: Resilience Software Design
---

## What does Resilience mean?  ##

>  In [computer networking](https://en.wikipedia.org/wiki/Computer_network): **resilience** is the ability to provide and maintain an acceptable level of [service](https://en.wikipedia.org/wiki/Service_(systems_architecture)) in the face of [faults](https://en.wikipedia.org/wiki/Fault_(technology)) and challenges to [normal operation](https://en.wikipedia.org/w/index.php?title=Normal_operation&action=edit&redlink=1). - Wikipedia

Failure does alwasy happen in the software world. A resilient system would automatically cut off failing components and reintegrate them once they are no longer failing.

## Principles of API Resiliency 

> Here are some of the key principles that informed our thinking as we set out to make the API more resilient.
>
> 1. A failure in a service dependency should not break the user experience for members
>
> 2. The API should automatically take corrective action when one of its service dependencies fails
>
> 3. The API should be able to show us what’s happening right now, in addition to what was happening 15-30 minutes ago, yesterday, last week, etc.
>
>    ​                    — from Netflix techblog

## Patterns ##

### Timeout ###

> - **Apply to Integration Points, Blocked Threads, and Slow Responses**  The Timeouts pattern prevents calls to Integration Points frombecoming Blocked Threads. Thus, they avert Cascading Failures.
> - **Apply to recover from unexpected failures**  When an operation is taking too long, sometimes we don’t carewhy...we just need to give up and keep moving. The Timeouts pat-tern lets us do that.
> - **Consider delayed retries**  Most of the explanations for a timeout involve problems in thenetwork or the remote system that won’t be resolved right away.Immediate retries are liable to hit the same problem and result inanother timeout. That just makes the user wait even longer for hiserror message. Most of the time, you should queue the operationand retry it later.

### Circuit Breaker ###

![Circuit Breaker](https://i-msdn.sec.s-msft.com/dynimg/IC709532.png)

> The Circuit Breaker pattern can prevent an application repeatedly trying to execute an operation that is likely to fail, allowing it to continue without waiting for the fault to be rectified or wasting CPU cycles while it determines that the fault is long lasting. The Circuit Breaker pattern also enables an application to detect whether the fault has been resolved. If the problem appears to have been rectified, the application can attempt to invoke the operation.

### Bulkheads###

![Bulkheads](http://image.slidesharecdn.com/resiliencepatterns-141105153710-conversion-gate02/95/patterns-of-resilience-25-638.jpg?cb=1454361598)

