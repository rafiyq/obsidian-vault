## What is Concurrent Programming?

Multiprocessing, Concurrent, Parallel, and Threaded programming are all synonymous. Modern programming is built around maximizing the utilization of the multiple processors and cores of modern computers and the best way to do that is via running multiple processes and threads. This is done without developer intervention by the operating system, but you have the ability to improve the efficiency of your software by writing quality code with threads that process data independently.

Some highly complex tasks such as artificial intelligence, audio/video processing, and signals processing can be written with multiprocessing in mind, but beware as this can go awry. Parallel programming has been the basis of software that requires lots of computing power but also allow for asynchronous interactions with the user.

## What is a thread?

It is an independent collection of sequentially executed programming steps. Think of a program with multiple independent threads like train tracks that separate and come together at certain points, when the tracks are apart multiple trains can go as fast as they want but when they are together each train is limited by the speed of the train in front of it.

With modern CPUs (laptops or consumer desktops), you will often have 4-8 cores and each core can have 1-4 threads managed by the scheduler. The heart of any OS’s multithreaded capability is the scheduler which shuffles different programs (including OS tasks) between active and inactive states and moving them between cores, moving data around caches, etc.

Computers have multiple levels of memory from the HD to registers shared between cores, they allow for common data amongst threads (even the instructions that multiple of threads from the same program execute). The goal of memory caching is to limit the amount of time that is spent waiting for data/instructions to be retrieved from slower and more distant caching, which causes threads to become inactive.

## Thread Scheduling

![[Picture2.webp]]

What we see in this diagram is a CPU scheduler shifting between threads on different cores. In this case presume that all 4 cores are on the same processor and share at least an L2 cache.

Why are threads made inactive and shifted between cores?

They have their state changed due to cache misses and the scheduler doesn’t want to waste CPU cycles on waiting for data/instructions, so instead find something that needs to be run and make it active. There is of course lost time in switching between threads, so constantly switching has a cost as well.

## Memory Caching

Memory Caches are hierarchical in nature and they really work on the principle that memory that is physically closer is more performant.

![[Picture1.gif]]
Figure 1 Shared Cache Example: A dual-core, dual-processor system[^1]

Caches are not just used for storing localized data/instructions for a CPU, but it also is used as a sharing mechanism between cores and as a way to store data/instructions that limit the number of times that requests have to go to RAM or even hard drive space.

There are L3 caches but apply a little less when we get to GPUs and won’t be discussed in detail here.

[^1]: Tian, Tian and Shih, Chiu-Pi. 2012. Software Techniques for Shared-Cache Multi-Core Systems. Retrieved from [https://software.intel.com/content/www/us/en/develop/articles/software-techniques-for-shared-cache-multi-core-systems.html?wapkw=smart+cache](https://software.intel.com/content/www/us/en/develop/articles/software-techniques-for-shared-cache-multi-core-systems.html?wapkw=smart+cache)
