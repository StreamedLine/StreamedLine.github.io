---
layout: post
title:      "Styling Code "
date:       2018-06-28 04:38:34 +0000
permalink:  styling_code
---


## With some help from Google

### It's a 2 step process

### 1
Add the following script to the head.
```
<script src="https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js"></script>
```

### 2
Add the class name 'prettyprint' to the `<pre>` element you'd like to have code in.

### example
(Notice i've added the class linenums as well. it adds numbers to the lines)

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Styling Code</title>
	<script src="https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js"></script>
</head>
<body>

<pre id="codeHTML" class="prettyprint linenums">
    function insertionSort(arr) {
		for (var i = 1; i < arr.length; i++) {
			let currentVal = arr[i];
			let j = i - 1;
			while (j >= 0 && arr[j] > currentVal) {
				arr[j + 1] = arr[j];
				console.log(arr)
				j = j - 1; 
			}
			arr[j + 1] = currentVal;
			console.log(arr)
		}
		return arr
	}
		
     function quickSort(arr) {
		if (arr.length <= 1) {
			return arr
		} else if (arr.length == 2) {
			let smaller = Math.min(arr[0], arr[1]);
			let larger = Math.max(arr[0], arr[1]);
			return [smaller, larger]
		}
		let pivot = arr.shift();
		let smallerVals = [];
		let largerVals = [];
		for (let i of arr) {
			if (i < pivot) {
			 	smallerVals.push(i)
			} else {
				largerVals.push(i)
			}
		}
		return quickSort(smallerVals).concat(pivot, quickSort(largerVals))
	}
</pre>
</body>
</html>
```

### Bonus (I lied. 2 more steps)

### 3
Google the following: **code prettify themes**

### 4
Download a theme and put it into a separate CSS file (don't forget to link it from your HTML file)

## Something crazy I like to do
Sometimes I have an HTML file with only a script (for the browser debugger tools) and I like seeing the code on the page while having it live in the console.

I do this by dynamically inserting a script into my styled `pre` element, so the moment I update the javascript, it's updated in both places.

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Sorting algorithms</title>
	<script src="https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js"></script>
	<link rel="stylesheet" href="styles.css">
</head>
<body>
<h3>The following code is live in the console</h3>

<pre id="codeHTML" class="prettyprint linenums">
</pre>
<script id="codeScript">
	
	function insertionSort(arr) {
		for (var i = 1; i < arr.length; i++) {
			let currentVal = arr[i];
			let j = i - 1;
			while (j >= 0 && arr[j] > currentVal) {
				arr[j + 1] = arr[j];
				console.log(arr)
				j = j - 1; 
			}
			arr[j + 1] = currentVal;
			console.log(arr)
		}
		return arr
	}
		

	function quickSort(arr) {
		if (arr.length <= 1) {
			return arr
		} else if (arr.length == 2) {
			let smaller = Math.min(arr[0], arr[1]);
			let larger = Math.max(arr[0], arr[1]);
			return [smaller, larger]
		}

		let pivot = arr.shift();
		let smallerVals = [];
		let largerVals = [];
		for (let i of arr) {
			if (i < pivot) {
			 	smallerVals.push(i)
			} else {
				largerVals.push(i)
			}
		}
		return quickSort(smallerVals).concat(pivot, quickSort(largerVals))
	}

</script>
<script>
	let code = document.querySelector('#codeScript').innerText.split('\n');
	if (code[0] === '') {
		code.shift();
	}
	document.querySelector('#codeHTML').innerHTML = code.join('\n');
</script>
</body>
</html>


```


