There are three main libraries in the standard Python 3 programming language distribution, though numerous other libraries can be downloaded that work similarly. We will only go over these three since they are available out of the box and very well supported.

- The \_thread and threading libraries are low and high-level interfaces to Python 3 threads.
- Asyncio is a library implementing a number of core functionality for asynchronous execution of code.
- Lastly multiprocessing is a library that aims to go beyond just threads for concurrent software.

## \_thread/threading Libraries

To make the \_thread or threading libraries, just add an import statement at the top of your .py file for overall access or at the top of your method for method-level access to these libraries.

Threads are started with the `start_new_thread` method, which you pass the name of the function that the thread will execute, and then the argument and finally keyword-based arguments that map to the args/kargs of the named function. This acts as shorthand for the the run and start methods, which may be extra boilerplate code.

When using the \_thread library you can take the returned value of the `start_new_thread` or similar function, which is a handle on the started thread, and lock, acquire a lock and then release the lock on a critical section of code. This is a very common pattern of use for locks on critical code sections.

Semaphores can be used to signal access to a variable, by default a single thread at a time, or a BoundedSemaphore can be used to allow a predefined number of threads to access a variable.

There is also a scheme for communication between threads using events and event handling.

Lastly a Barrier can be placed in code, to make sure that all active threads execute up to but not beyond the Barrier prior to all threads hitting the barrier. This is a good way to synchronize data, especially if one or more variables need to have a coherent value across multiple threads.

## asyncio Library

Asyncio is a common language construct among multiple languages, which allows in a very simple manner for management of asynchronous code.
### Basic Syntax

```python
import asyncio  
import time

async def say_after(delay, what):
	await asyncio.sleep(delay)
	print(what)

async def main():
	print(f"started at {time.strftime('%X')}")
	await say_after(1, 'hello')
	await say_after(2, 'world')
	print(f"finished at {time.strftime('%X')}")  
  
asyncio.run(main())
```

Once imported, functions can use the `async` keyword to indicate that they may be executed in an asynchronous fashion. Think of this like the situation when your code wants to get information from a networked server, but you don’t need to have your whole system wait for the execution of one or more lines of code.

There is some guarantee that the async’d method will eventually complete and the library will handle this.

Back in the Python 2 days, web applications that made time intensive processing in the middle of a call for data from your browser would either have to sit and wait or ask Python 3 became more available, developers monkey patched this library into Python 2 code, not pretty.

To call the function and let it execute in its own thread, the calling code just needs to wrap the async method in the `asyncio.run` method.

Alternatively if you want the code to wait for the execution of an async method, the `await` keyword is used, common when sleeping a thread.

### Advanced Syntax

```python
import asyncio

async def async_func1():
	return 42

async def async_func2():
	return 6*7

async def main():
	task = asyncio.create_task(async_func1())
	await task
	await asyncio.gather(async_func1(), async_func2())
	await asyncio.sleep(1)

asyncio.run(main())
```

Some more advanced capabilities of asyncio, include creating tasks. Unlike the run call that returns the method that is called by the thread, `create_task` not only executes the coroutine but returns a task object that can be used to retrieve results.

A task can be used as part of a sequence of calls that can be executed in parallel with the gather method.

The `sleep` method is very important as it allows for executing threads to wait a predetermined amount of time. This is handy if your code to do something aside from handle the result of a calculation, but will want to wait for a result to eventually be returned.

Also, if you want to have threads that have a loop that is executed as long as they exist, think of polling the filesystem for change and then performing a calculation or showing the contents of a file in an application window.

## multiprocessing Library

This library is very powerful, as it takes the idea of independent execution of threads inside of a Python 3 context and allows for execution of code outside of the current calling process and even on a remote machine.

spawn, fork, and forkserver all have similar general goals create new processes outside of the current process, though they have slightly different results.

Spawn is the most basic version, create a new python interpreter process, which will be similar but not the same as the current process, basically the python interpreter with existing libraries.

Fork is more of a copy of the current process, though it can change over time.

Forkserver is the most elaborate. It creates a server that when called forks a new process, so it can be called repeatedly.

It also handles any dead processes that may occur over time.

The constructor for a Process is very similar to how you create threads in other libraries, you pass keyword arguments for the target function to be executed and args that will be passed to the associated method.

To begin the processes execution you call start and when you want to halt the calling threads execution until the processor is done call join.

For processes to be able to communicate with each other, either a queue or pipe can be passed as an argument to the various processes,

Queues are sequentially accessible data structures and pipes are two-way mechanisms for communicating between two ends of the pipe.

It is possible to have more than two processes access the same end of the pipe, but simultaneous read writes will corrupt the queue, so if you want multiple read writes between a parent and child processes, it might make more sense to use multiple queues.

Like with the two previously mentioned thread libraries, the lock, acquire and release object and functions can be used to manage access to critical sections of code.
### Basic Syntax

### Data Sharing

To share data between multiple threads you can use the Value object for a single value object to be shared and Array to share a collection of primitives.

If you would like to spin up multiple processes for constantly completing work, a worker pool is a common pattern.

You create a Pool object , with the number of processes that you would like to be spawned, then each time you want to have parallel execution by the pool, just perform functions on the pool like map, which has a function and an array of values passed and then pool workers execute the function with a value in the array until the array has been completely mapped.

This form of functional programming is becoming more common and programming languages handle them efficiently.

There are also other common primitives like in the \_thread/threading libraries but of course they execute beyond the score of the current process but across any spawned/forked processes.

## Bibliography

[1] tutorialspoint.com. 2020. tuturialspoint Python 3 – Multithreaded Programming. Retrieved from https://www.tutorialspoint.com/python3/python_multithreading.htm
[2] python.org. 2020. docs.python.org asyncio. Retrieved from https://docs.python.org/3/library/asyncio.html
[3] python.org. 2020. docs.python.org multiprocessing. Retrieved from https://docs.python.org/3/library/multiprocessing.html

## External Resources

MachineLearningPlus Parallel Programming in Python [web page](https://www.machinelearningplus.com/python/parallel-processing-python/ "Python Parallel Programing Tutorial")