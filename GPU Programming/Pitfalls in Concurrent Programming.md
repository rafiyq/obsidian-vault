There are many issues that can occur if care isn’t taken when writing concurrent programs. They include race conditions, dead and live lock, non-optimal resource utilization, and content over resources

## Race Conditions

One of the most common pitfalls that you will encounter when writing multithreaded programs is a race condition. This occurs when threads execute in a sequence different than intended and can have dire consequences.

![[GPU_prog_race_contention.svg]]

In this case the programmer wanted the first thread to execute its 3 instructions and then the second thread to execute its 3 instructions. Unfortunately the instructions were interleaved and therefor the final integer value is not what the developer wanted.

I want to make it clear that in this case there isn’t an incorrect final value, since each thread performed its instruction in a valid manner related to the shared variable. It is often best to consider minimizing shared or global variables or if they are required have a plan to ensure that each thread’s access is atomic, which we will talk about later.

## Resource Contention

Similar to a race condition, but more related to memory and not the order of execution, is resource contention. The more threads and shared resources, the more often this will occur, if the programmer doesn’t give sufficient consideration to this happening.

![[GPU_prog_resource_contention.png]]

This is a more asynchronous version of a race condition, which can extend from threads to completely separate machines. What happens is that resources are needed to be accessed in different ways by different independent threads and they access the same memory, file, etc. and this can lead to conflict and constant rewriting of values.

Consider the case of databases where values need to be incremented but each time a value is retrieved from the database another thread is accessing the same row. Now it can happen that between the time that the first thread accesses and updates the row and n threads do the same thing, that numerous increments go uncounted since the last updated value is what is counted. This is significant enough of an issue with databases, that they have numerous ways of ensuring consistency.

## Dead Lock

Deadlock is similar to resource contention, except that one or more threads or processes require multiple shared resources and will not perform their action until they have access to all required resources.

![[GPU_prog_dead_lock.png]]

At the same time they need other required resources they do not relinquish their hold on a shared resources.

Now multiple threads each have a shared and required resource and simultaneously are waiting for other resources and cannot proceed to the point when they can release their resources.

None of the participants in the deadlock will make it out of this situation.

The first response is to have threads drop the holds on resources, but this will devolve into threads dropping resources and then frantically trying to get all of the resources and possibly not help at all.

## Live Lock

Live Lock is **like deadlock but each thread is actively doing something** but never makes it out of the overall process that requires multiple resources.

This can happen when a programming loop tests for access prior to making a final change and goes to sleep for a small or no time.

![[GPU_prog_live_lock.png]]

Consider a do-while loop that doesn’t change an externally visible display until it can save the value to a resource.

Numerous threads executing the same loop might come to the while test and not be able to access the variable, and thus keep incrementing a variable, this could result in buffer/stack overflows or executing an instruction millions or infinite amount of times or recursively executing the same code and locking up a program.

This can even happen if you incorrectly use some programming language asynchronous capabilities.

## Resource Over/Under Utilization

A slightly less worrisome issue is over or underutilizing the computational power of your machine, though if this happens with a very powerful system or replicated over a large cluster of computing resources, this can be expensive.

So as the name should indicate, this is when you have too few or too many threads and they have nothing to do or the few threads are performing a series of computations that could be broken down and run in parallel.

If too many threads are going from active to inactive status, due to not having work to do, the cost for context switching can outweigh the speed offered when many threads are being used.

This can be handled by scaling the number of threads based on the amount of data or CPU utilization.

When threads are too few, they may be in constant use and small memory leaks or inefficiencies can compound and CPU utilization may spike which makes all running threads slower.

Also if a thread requires a lot of data or lots of instructions, cache hits can occur more frequently and therefor the system will be slowed by data transfers to/from the cache to RAM or worse even the hard drive.

## Bibliography

§[1] Wikipedia. 2020. WikipediA: the Free Encyclopedia. Retrieved from [https://en.wikipedia.org/wiki/Race_condition#Software](https://en.wikipedia.org/wiki/Race_condition).

§[2] Geeks For Geeks. 2020. Introduction of Deadlock in Operating System. Retrieved from [https://www.geeksforgeeks.org/introduction-of-deadlock-in-operating-system/](https://www.geeksforgeeks.org/introduction-of-deadlock-in-operating-system/).