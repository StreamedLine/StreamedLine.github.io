---
layout: post
title:      "Sorting Arrays With Javascript"
date:       2018-07-11 03:54:40 +0000
permalink:  sorting_arrays_with_javascript
---

## Bubble and Insertion Sort

I spent the last 2 weeks reviewing basic sorting algorithms.

Feel free to skip the next few lines and jump straight to the code!

Every algorithm has its pros and cons, depending on the scenario.

If an array is almost completely sorted Bubblesort will do a great job, if the array isn't almost completely sorted Bubblesort will take many more steps to complete the job.

What interests me however, is being able to visualize, in an intuitive way, how the algorithm is actually going to sort the array.
What helped me do that, was to write a [tool](http://mystic_turtles.surge.sh/) that visually shows how the array is being sorted. I recommend people write their own, since this was a fun and helpful project for me.

## Bubblesort

Consider this unsorted array: [9,5,2,3,4]

Notice how the digit 9 'bubbles' to the right!
[**9**,5,2,3,4]

[*5*,**9**,2,3,4]

[5,*2*,**9**,3,4]

[5,2,*3*,**9**,4]

[5,2,3,*4*,**9**]

It goes from left to right, and compares each element to the one after it. if the element is larger than the one after it - it swaps them.

In the above example, we now know that the last element is sorted!
In the next loop we will still start from index 0, but move right only until array.length -2.
We continue looping until there is nothing left to swap or until we reach array.length - array.length.

Let's continue our example:

[**5**,2,3,4,9]

[*2*,**5**,3,4,9]

[2,*3*,**5**,4,9]

[2,3,*4*,**5**,9]

And we are done!

### Code

```
function bubbleSort(arr) {
  for (let i = arr.length; i > 0; i--) {
	  let swap = false;
  	for (let j = 0; j < i; j++) {
	  	if (arr[j] > arr[j+1]) {
			  //swap
		  	let temp = arr[j];
			  arr[j] = arr[j+1];
		  	arr[j+1] = temp;
				
		  	//if swap would be false after this loop, it means the array is sorted
			  swap = true;
		  }
	  }
	  if (!swap) {break }
  }
	
	return arr
}
```

To visualize [click here](http://mystic_turtles.surge.sh/bubble)


## Insertion Sort

Consider this unsorted array: [9,5,2,3,4]

[9,5,2,3,4]

[5,9,2,3,4]

[2,5,9,3,4]

[2,3,5,9,4]

[2,3,4,5,9]

What just happened?

Let's break this down.

The algorithm creates a 'sorted zone' that gets bigger with each element it encounters.

The first element it encounters is 9

[**9**,5,2,3,4] => sorted zone is now the first element [sorted, unsorted, unsorted, unsorted, unsorted]


next element is 5. Let's move it into the sorted zone!

[**5**,**9**, 2, 3, 4] => sorted zone is now the first two elements [sorted, sorted, unsorted, unsorted, unsorted]


next element is 2. Let's move it into the sorted zone. this will involve shifting 9 and 5 to the right.

[**2**,**5**, **9**, 3, 4] => sorted zone is now the first three elements [sorted, sorted, sorted, unsorted, unsorted]


next element is 3. Let's move it into the sorted zone. this will involve shifting 9 and 5 to the right.

[**2**,**3**, **5**, **9**, 4] => sorted zone is now the first four elements [sorted, sorted, sorted, sorted, unsorted]


next element is 4. Let's move it into the sorted zone. this will involve shifting 9 and 5 to the right.

[**2**,**3**, **4**, **5**, **9**] => sorted zone is now the entire array [sorted, sorted, sorted, sorted, sorted]

### Code

```
function insertionSort(arr) {
  for (var i = 0; i < arr.length; i++) {
	  //save current positions value
    let temp = arr[i]
		
	//if values are larger- shift them to the right
    let j = i - 1;
    while (j >= 0 && arr[j] > temp) {
      arr[j+1] = arr[j]
      j -= 1; 
    }
		
	//when done shifting- drop element in 'sorted zone'
    arr[j+1] = temp
  }

  return arr
}
```

To visualize [click here](http://mystic_turtles.surge.sh/insertion)

