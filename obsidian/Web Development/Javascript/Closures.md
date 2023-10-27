## What is a closure?
A **closure** is the combination of a function bundled together (enclosed) with references to its surrounding state (the **lexical environment**).

Very basic:
```js
var x = 1
function foo(){
	console.log(x)
}
foo() // 1
```

Example:
```js
function numberGenerator() {
  var num = 1;
  // Local variable that ends up within the closure.
  function checkNumber() { 
    console.log(num);
  }
  num++;
  return checkNumber;
}

var number = numberGenerator();
number(); // 2
```

## Scope Explained:
Scope refers to the locations where a variable is visible.

example:
```js
function foo(){
	var boop;
	// boop is within bar() scope
	function bar(){
		var beep;
		// beep is not within foo() scope
	}
}
// bar() is a closure which consists of the function bar() and the variable (boop) created in foo()
```

Example of the use of closures:
```js
var result = [];
 
for (var i = 0; i < 5; i++) {
  result[i] = function () {
    console.log(i);
  };
}

result[0](); // 5, expected 0
result[1](); // 5, expected 1
result[2](); // 5, expected 2
result[3](); // 5, expected 3
result[4](); // 5, expected 4 
```

As we see, all functions in the result array log out 5. Why is this?
The functions in the result array all use the same scope from the for-loop. This scope is updated on each iteration of the loop and then used by the functions when they are called.

One way we can fix this using closures:
```js
var result = [];
 
for (var i = 0; i < 5; i++) {
  result[i] = (function inner(x) {
    // additional enclosing context
    return function() {
      console.log(x);
    }
  })(i);
}

result[0](); // 0, expected 0
result[1](); // 1, expected 1
result[2](); // 2, expected 2
result[3](); // 3, expected 3
result[4](); // 4, expected 4
```

Here we are passing the variable 'i' to the 'inner' function and then returning the new function which now uses the scope from the inner function. So when we call the functions from the result array each function will use the 'x' variable from the inner function scope.

Another real-world example of closures you will commonly find are using the fetch() function

Example:
```js
function outerFunction(url, x){
	fetch(url).then(() => {
		console.log(x)
	})
}
// fetch(), being an asynchronous function, will await a response and then run the arrow function.
// The console log still has access to the 'x' variable after the outer function has completed
```


Links:
Simple explanation:
https://www.youtube.com/watch?v=3a0I8ICR1Vg

In-depth explanation:
https://www.freecodecamp.org/news/lets-learn-javascript-closures-66feb44f6a44/