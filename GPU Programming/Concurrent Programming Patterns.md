Many of the solutions to parallel programming challenges fit into these 5 patterns: Divide and Conquer, Map-Reduce, the repository, pipelines or workflows and recursion. Learning to recognize that one of these patterns can be used in your program to make it more efficient and you will save yourself a lot of time, avoiding trying to reinvent the wheel

## Divide and Conquer

One of the most common ways to solve computer science problems, even without concurrency, is divide and conquer. You probably have seen how it can be used in search and sorting algorithms.

![[devide_and_conquer.png|500]]

The basic idea is to split up the data until it is small enough to answer the larger question (order or equality) for the smaller amount of data. Once the thread has that answer, return that answer to what called it and it will take the responses from all of the smaller data sets and answer the question with less work. This makes it back to the main calling context and it should have taken less time than doing pairwise comparisons.

It is not always the best answer, finding the same value in a set might take N comparisons, and thus if the data set is not already sorted you will pay an extra cost for the breaking down and bringing back together. If recursion is not allowed or really inefficient, which is the case in CUDA, then this should be used sparingly.

Also, a program implementing this will need to be well-designed and/or maintain a complex state for all of the various divides, etc.

## Map-Reduce

Map-Reduce can be thought of as a subset of divide and conquer. The main difference is that each time a map-reduce cycle is run, it immediately breaks down into individual data points and the same operation is applied to all individual pieces of data. Each mapper returns only 1 value and the reducer has the job of taking N return values and reducing it to a single value.

![[map-reduce.webp|500]]

An example would be testing if a value is in a set. Each mapper would return a 0 if the value passed to it was not the searched for value and 1 if it is. The reducer would just add all the values and convert 0 to false and greater than 0 to true.

The nice thing about this way of doing things is that it scales well regardless of size of data and quality of computing resources, presuming the MR system is well architected and communications is not slow. What mappers and reducers do can be more complex or they can be strung into a series of MR jobs that feed into each other.

## Repository

The repository pattern can be used when state needs to be maintained across multiple threads or processes. Each process can run independent and when it needs information or wants to change the overall state, it makes requests of the repository.

![[repository.webp|500]]

The repository needs to ensure that data is managed atomically within itself, but processes are responsible for maintaining their own state.

Based on concerns of data consistency or staleness, this system may want to encourage more or less use of the repository, since it is possible for a process to work on data for a while and want to update it but doing so could overwrite changes that were made based on a newer state.

## Pipelines/Workflows

Pipelines and workflows are similar. They are both representable as directed graphs without cycles (though that is not strictly the case, since some workflow systems allow cycles but data will still flow out of a node).

![[pipeline.webp|500]]

Pipelines are workflows in which each step gets its input data from the previous step and outputs to a single future step.

Workflows often employ fan out and in patterns where either the same data is output to different logical steps or data is divided up and sent to the same logical code.

Note that map-reduce and divide and conquer can be implemented using workflows though neither are exclusive to the other, programming languages handle divide and conquer and map reduce especially now in a more functional programming way.

## Recursion

A key way to solving many complex problems can be via recursion. Almost any problem can be solved recursively, though not always most efficiently.

![[recursion.webp|320]]

Functional programming languages and frameworks such as Lisp, Clojure, and Lodash are built around some level of recursion. In these cases data is divided into head and tail or first and rest.

Functions operate on the current data and call themselves with the rest. Recursion does not have to be handled in that way. It can be divided in a number of ways including in a binary manner.

Recursion requires management of state, since you need to ensure that isn’t infinite, which means that recursive algorithms need final states, often when only 1 or 2 pieces of data are inputs to a function.

Recursion is not advisable when you are using it on large data across multiple local or distributed CPUs not on the same processor and GPUs don’t perform well in this pattern.

## Parallel Programming Resources

Cornell University - Functional Programming with OCaml Open Source Textbook - [Concurrent Programming Chapter](https://www.cs.cornell.edu/courses/cs3110/2019sp/textbook/ads/concurrency.html)

## Bibliography

[1] Kim, Eun-Gyu. 2004. Department of Computer Science, University of Illinois. Parallel Programming Patterns. Retrieved from http://snir.cs.illinois.edu/patterns/patterns.pdf 