To show how you can create code to search for a value in a data set, with serial and parallel means, we will use some pseudocode to illustrate how this can be done.

Search is one of the most canonical challenges of computing, so understanding good and bad ways to perform it can help define other analogous processes using sequential or concurrent programming

Also, as a means of breaking down what types of programming work for what type of data, we will investigate Flynn’s Taxonomy.

## Serial Search Pseudocode

### Inefficient Serial Search

In this code, you will recognize a very simple sequential algorithm for finding the index of a searched value in a set of data.

```c
int[] data = [ 1, 6, 9, 2, 3, 5, 4 ];
int foundIdx = serialSearch(data, x);

int serialSearch(data, searchValue){
	int foundIndex = -1;
	for (int i = 0; i < data.length; i++) {
		if(data[i] == searchValue){
			foundIndex = i;
			break;
		}
	}
	return foundIndex;
}
```


Simply stated, iterate through all values in the set and the search value is equal return the index, otherwise -1 or not found will be returned.

So the good things are that it is pretty much the simplest implementation that you could imagine and there is no need to sort the data ahead of time, which can be costly.

The negative is that to find the index, based on the data and the value passed, you may need to search through all values in the data set.

Linear search is not great, especially if you do a lot of search.

That is why the cost of sort along with a good (logarithmic based on the data set size) is preferred, even if there is a large initial cost, especially if the data set can be updated efficiently.

### Recursive Serial Search

```c
int[] data = [ 1, 2, 3, 4, 5, 6, 9 ];
int foundIdx = binarySearch(data, 0, data.length, x);

int binarySearch(int arr[], int l, int r, int x) 
{ 
	if (r >= l) { 
		int mid = l + (r - l) / 2; 
		if (arr[mid] == x)
			return mid; 
		if (arr[mid] > x) 
			return binarySearch(arr, l, mid - 1, x); 
		return binarySearch(arr, mid + 1, r, x); 
	}
	return -1;
} 
```

This is one of the more common implementations of search and is a divide and conquer solution.

We will presume that no matter what data is, it is always sorted or this will not work.

The code divides and conquers the search by picking midpoints which are tested to see if they are equal to, larger, or smaller than the searched value.

If not equal the function calls itself with the left or right subsets (each one being smaller than the calling functions data set.

If nothing is found return -1.

The positive aspects of this implementation is that search become logarithmic and if the cost of sort is low relative to the follow-on usage of search than it is worth the upfront cost.

If the sort doesn’t update efficiently or the data and/or computation is distributed this becomes a very negative cost.

## Parallel Search Pseudocode

```c
int[] data = [ 4, 6, 7, 1, 2, 8 ];
int numElements = ceil(data.length / numThreads);
Thread[] threads = new Threads[numThreads];
for (int tIdx = 0; tIdx < numThreads; tIdx ++) {
	int startIdx = tId*numElements;
	int endIdx = startIdx + numElements;
	int[] sData = slice(data, startIdx, endIdx);
	int i = threads[tIdx].start(pSearch(sData, x);
}

int pSearch(data, x) {
	for (int idx = 0; idx < data.length; idx++) {
		if(data[idx] == x) {
			killOtherThreads();
			return idx;
		}
	}
}
```

The first thing you will notice about the parallel search is that it is more complex since you need to assign correct data to each thread — in this case that is by uniformly slicing up the data into subsets to evenly distribute the load to each thread.

Each thread only searches a smaller subset of data and if it finds x, then it needs to kill the other threads (probably indirectly) and return the index.

Good parts of this are that no sorting is required and scaling can be managed by increasing the number of threads.

The negatives are that if the number of threads is order of magnitudes small than the data size, this is just slightly more efficient than the inefficient serial search.

Thread management isn’t easy and killing off other threads would either be dangerous or require well thought out logic.

This could be improved with presorting and binary search but then it would inherit the issues with recursion.

Where this shines is if you have lots of threads and that is where GPUs come in, more on that later, but if each thread just needs to do a single comparison and only update a shared variable if it is found, then you have a constant search time (better than logarithmic).

## Flynn’s Taxonomy

So let’s look at Flynn’s taxonomy.

![[flynn_taxonomy.webp]]

The first two characters can be either SI or MI, single or multiple instruction, which means do you perform the same logic or different logic on all data.

The second two characters can be either SD or MD, single or multiple data, which means is the data complex or is it numerous and simple.

In the top left are sequential programs working on a single complex state.

Think of this as a program that executes a chess or non-trivial game between two humans, lots of parts but the game probably cannot be decomposed. This isn’t about searching for the next move, just managing state.

The bottom right are problems multiple different processes are doing different things to lots of small pieces of data. 

This is similar to running multiple filters on pixels in an image or images in a video or something similar.

Each operation may be completely independent of the other and may not need context like previous images in a sequence or values for nearby pixels.

Most CPU-based sequential programs are MISD, since they have multiple different processing steps that are meant to work on a single or few complex objects.

GPUs and other distributed programming solutions are often SIMD, since they aim to use numerous threads and processes running the same logic on large amounts of data.

Use this taxonomy to look at your data and what you are trying to do and then when you determine which of the 4 is your category, look at applicable languages, frameworks, hardware, etc.

## Bibliography

[1] Geeks For Geeks. 2020. Binary Search. Retrieved from https://www.geeksforgeeks.org/binary-search/.
[2] Mark Ilg, Jonathan Rogers, and Mark Costello. 2011. Projectile Monte-Carlo Trajectory Analysis Using a Graphics Processing Unit. In AIAA Atmospheric Flight Mechanics Conference, August 8 – 11, 2011. Portland, Oregon. https://doi.org/10.2514/6.2011-6266

## External Resources

GeeksForGeeks Flynn’s Taxonomy [web page](https://www.geeksforgeeks.org/computer-architecture-flynns-taxonomy/ "Flynn's Taxonomy")