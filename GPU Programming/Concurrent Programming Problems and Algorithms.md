4 canonical challenges and algorithms in the world of parallel programming are dining philosophers, producer-consumer, sleeping barber and also data and code synchronization (more of a parallel programming mechanism).

Each of these are at the heart of different issues that you will encounter and a solution for them will solve numerous analogous issues, so keep them in mind as a pattern to look for when programming with parallelism.

## Dining Philosophers

I hope you enjoy this depiction of the dining philosophers problem, using Ron Swanson from Parks and Rec, which seems a little less scary than having Socrates and Plato waiting to eat.

![[dining_philosophers_problem.webp]]

So each philosopher wants to eat but they need two forks to be able to do this.

Don’t ask me why they need two forks but they do.

They can only do one thing at a time, pick up one fork, eat eggs, put a fork down, etc.

So they need to eat with both and in a naive implementation, where a philosopher tries to pick up the left fork and then the right and then eat and put forks down, will fail since this will most probably result with each philosopher having one fork and hangry!

Does this seem familiar? It is a little bit of a few of the pitfalls encountered in the previous video.

If you expect each philosopher to neatly and politely get forks and eat without ever trying to pick up the same fork then it is resource contention (with the fork being the resource).

If you have the philosophers hold their ground and never drop a fork then it is dead lock, almost literally.

If each philosopher drops the fork they hold and tries to get the other fork then you probably have live lock.

Consider a way to solve this? Could the philosophers communicate to each other or have a central authority determine the order.

There are many solutions to this problem but they aren’t always easy, so think before writing code.

## Producer-Consumer

Producer consumer or reader writer pattern is a very common tool these days.

![[producer_customer_problem.webp|500]]

A very common way this is used is in message queues, which allow for data to be added sequentially, non-sequentially, in a streaming or batch fashion. Then users pull or subscribe to the message queue and it returns data (either in order or as it becomes available). One or more processes, producers, can then add data to be consumed by the consumers.

If there are is more data than the queue can handle there are a number of strategies based on how the data is used.

If the most recent data is most important, then the queue will drop the oldest data.

If only a subsampling of data is needed, then data can be randomly dropped from the queue.

If all data is important than newer data can be stored for access (slower and less costly) when space is available or consumers can be told to hold back.

There is a chance of race conditions if the data structure or queue allows for overwriting of values or the pointer/index for the producer ends up being ahead of the index for the consumer and thus a producer may never end up with new data.

## Sleeping Barber

The sleeping barber is similar to producers consumers but order is not important, the threads are trying their best to optimize the barbers work.

![[sleeping_barber_problem.webp|500]]

The waiting room is like the queue/data structure from the previous slide, but the barber or barbers can only put one customer in the chair.

The waiting room is finite in size and two issues can occur.

First if the barbers are chatty and slow at cutting hair and there are lots of prospective customers we can have something like live lock or over utilization, where they stick there head in and see the waiting room full and leave.

The second major case is that there are no customers and the barbers just sit around sleeping and talking about how much better baseball was back in the day. This is a situation of underutilization.

There are solutions to this problem for one or more barbers, but when I think of this problem I think about inverting the problem and having the number of customers in the waiting room determine the number of barbers.

## Data and Code Synchronization

Many, if not most, languages provide a mechanism for synchronizing data or code.

This generally locks access to data or code, so use it with caution, if you make all data synchronized you end up with dead or live lock.

So if a thread attempts to access a synchronized piece of data, any thread that requires that data will wait.

This is useful in ticketing systems where you want to lock access to code or data until it has been fully used by the previous holder of the called ticket.

Semaphores are implemented with locks, but have a limited number of states to manage access to data or code more indirectly and allow for multiple accesses concurrently.

Think of this like seating categories for flights, those in class 1A can be seated.

Multiple individuals can board at the same time, which should minimize the possibility of being blocked by other passengers.

The major note here is there are rarely bulletproof solutions to multithreading problems but you can come up with a reasonable solution based on prioritization of coherent data access and acceptability of under or overutilization.

## Bibliography

[1] Adit.io. 2013. The Dining Philosophers Problem With Ron Swanson. Retrieved from [https://adit.io/posts/2013-05-11-The-Dining-Philosophers-Problem-With-Ron-Swanson.html](https://adit.io/posts/2013-05-11-The-Dining-Philosophers-Problem-With-Ron-Swanson.html).