# ES6 Iteration Methods
functional programming and Array iteration methods (forEach, map, filter, find, every, some, reduce)

- [forEach()](#forEach())
- [map()](#map())
- [filter()](#filter())
- [find()](#find())
- [every()](#every())
- [some()](#some())
- [reduce()](#reduce())

## Introduction
Several methods take as arguments functions to be called back while processing the array. When these methods are called, the length of the array is sampled, and any element added beyond this length from within the callback is not visited. Other changes to the array (setting the value of or deleting an element) may affect the results of the operation if the method visits the changed element afterwards. While the specific behavior of these methods in such cases is well-defined, you should not rely upon it so as not to confuse others who might read your code. If you must mutate the array, copy into a new array instead.


## forEach()
The `forEach()` method executes a provided function once for each array element.

```JavaScript
var images = [
  { height: 10, width: 30 },
  { height: 20, width: 90 },
  { height: 54, width: 32 }
];
var areas = [];

images.forEach(function(image) {
  var area = image.height * image.width;
  areas.push(area);
});
```

`forEach()` executes the provided callback once for each element present in the array in ascending order. It is not invoked for index properties that have been deleted or are uninitialized (i.e. on sparse arrays).

callback is invoked with three arguments:

- the element value
- the element index
- the array being traversed

## map()
The `map()` method creates a new array with the results of calling a provided function on every element in this array.

```JavaScript
// Using map, create a new array that contains the distance / time value from each trip.  
// In other words, the new array should contain the (distance / time) value.  
// Assign the result to the variable 'speeds'.

var trips = [
  { distance: 34, time: 10 },
  { distance: 90, time: 50 },
  { distance: 59, time: 25 }
];

var speeds = trips.map(function(trip) {
  return trip.distance / trip.time;    
});
```
`map` calls a provided callback function once for each element in an array, in order, and constructs a new array from the results. callback is invoked only for indexes of the array which have assigned values, including undefined. It is not called for missing elements of the array (that is, indexes that have never been set, which have been deleted or which have never been assigned a value).

Callback is invoked with three arguments: 
- the value of the element
- the index of the element
- the Array object being traversed

If a thisArg parameter is provided to map, it will be passed to callback when invoked, for use as its this value. Otherwise, the value undefined will be passed for use as its this value. The this value ultimately observable by callback is determined according to the usual rules for determining the this seen by a function.

`map` does not mutate the array on which it is called (although callback, if invoked, may do so).

```JavaScript
// Implement a 'pluck' function.  
// Pluck should accept an array and a string representing a property name 
// and return an array containing that property from each object. 

// example:
// var paints = [ { color: 'red' }, { color: 'blue' }, { color: 'yellow' }];
// pluck(paints, 'color'); // returns ['red', 'yellow', 'blue'];

function pluck(array, property) {
  var result = array.map(function(prop) {
    return prop[property];
  });
  return result;
}
```

## filter()

The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.

```JavaScript
// create a new array that only contains numbers greater than 50.
var numbers = [15, 25, 35, 45, 55, 65, 75, 85, 95];

var filteredNumbers = numbers.filter(function(number) {
  return number > 50;
});
```

```JavaScript
var users = [
 { id: 1, admin: true },  
 { id: 2, admin: false },
 { id: 3, admin: false },
 { id: 4, admin: false },
 { id: 5, admin: true },
];

var filteredUsers = users.filter(function(user) {
    return user.admin === true;
});
```

`filter()` calls a provided callback function once for each element in an array, and constructs a new array of all the values for which callback returns a value that coerces to true. callback is invoked only for indexes of the array which have assigned values; it is not invoked for indexes which have been deleted or which have never been assigned values. Array elements which do not pass the callback test are simply skipped, and are not included in the new array.

callback is invoked with three arguments:

- the value of the element
- the index of the element
- the Array object being traversed

`filter()` does not mutate the array on which it is called.

```JavaScript
// Create a function called 'reject'.  
// Reject should work in the opposite way of 'filter' - if a function returns 'true', 
// the item should *not* be included in the new array. 

var numbers = [10, 20, 30];

function reject(array, iteratorFunction) {
  return array.filter(function(el) {
    return !iteratorFunction(el);
  })
}

var lessThanFifteen = reject(numbers, function(number) {
  return number > 15;
}); 

lessThanFifteen // [ 10 ];
```

### find() 
The `find()` method returns a value of the first element in the array that satisfies the provided testing function. Otherwise undefined is returned.

```JavaScript
// Find the user in the users's array who is an admin.  Assign this user to the variable 'admin'.

var users = [
  { id: 1, admin: false },
  { id: 2, admin: false },
  { id: 3, admin: true }
];

var admin = users.find(user => user.admin);
```

The `find` method executes the callback function once for each element present in the array until it finds one where callback returns a true value. If such an element is found, find immediately returns the value of that element. Otherwise, `fin`d returns undefined. callback is invoked only for indexes of the array which have assigned values; it is not invoked for indexes which have been deleted or which have never been assigned values.

callback is invoked with three arguments: the value of the element, the index of the element, and the Array object being traversed.

```JavaScript
// Find the account with a balance of 12 and assign it to the variable 'account'.
var accounts = [
  { balance: -10 },
  { balance: 12 },
  { balance: 0 }
];

var account = accounts.find(account => account.balance === 12);
```

`find` does not mutate the array on which it is called.

```JavaScript
Write a 'findWhere' function that achieves this shorthand approach.  'findWhere' should return the found object.

var ladders = [
  { id: 1, height: 20 },
  { id: 3, height: 25 }
];

function findWhere(array, criteria) {
  return array.find(function(element) {
      var property = Object.keys(criteria)[0];
      return element[property] === criteria[property]
  });
}

findWhere(ladders, { height: 25 }); // result: { id:3, height: 25 }
```
### every()
The every() method tests whether all elements in the array pass the test implemented by the provided function.

```JavaScript
// Given an array of users, return 'true' if every user has submitted a request form.  
// Assign the result to the variable 'hasSumbmitted'.
var users = [
  { id: 21, hasSubmitted: true },
  { id: 62, hasSubmitted: false },
  { id: 4, hasSubmitted: true }
];

var hasSubmitted = users.every(user => hasSubmitted); 
console.log(hasSubmitted); // true // false
```

The `every` method executes the provided callback function once for each element present in the array until it finds one where callback returns a falsy value. If such an element is found, the every method immediately returns false. Otherwise, if callback returns a truthy value for all elements, every returns true. callback is invoked only for indexes of the array which have assigned values; it is not invoked for indexes which have been deleted or which have never been assigned values.
`every` does not mutate the array on which it is called.

### some()
The `some()` method tests whether some element in the array passes the test implemented by the provided function.

```JavaScript
// Given an array of network objects representing network requests, 
// assign the boolean 'true' to the variable 'inProgress' if any network request has a 'status' of 'pending'.

var requests = [
  { url: '/photos', status: 'complete' },
  { url: '/albums', status: 'pending' },
  { url: '/users', status: 'failed' }
];

var inProgress = requests.some(request => request.status === 'pending'); 
console.log(inProgress); // true
```
`some()` executes the callback function once for each element present in the array until it finds one where callback returns a truthy value (a value that becomes true when converted to a Boolean). If such an element is found, some() immediately returns true. Otherwise, some() returns false. callback is invoked only for indexes of the array which have assigned values; it is not invoked for indexes which have been deleted or which have never been assigned values.
`some()` does not mutate the array on which it is called.

### reduce() 
The `reduce()` method applies a function against an accumulator and each value of the array (from left-to-right) to reduce it to a single value.

```JavaScript
// Find the sum of all the distances traveled.  Assign the result to the variable 'totalDistance'

var trips = [{ distance: 34 }, { distance: 12 } , { distance: 1 }];

var totalDistance = trips.reduce(function(previous, trip) {
    return previous += trip.distance;
}, 0); 

console.log(totalDistance); // 47
```
`reduce` executes the callback function once for each element present in the array, excluding holes in the array, receiving four arguments:

- accumulator
- currentValue
- currentIndex
- array

The first time the callback is called, accumulator and currentValue can be one of two values. If initialValue is provided in the call to reduce, then accumulator will be equal to initialValue and currentValue will be equal to the first value in the array. If no initialValue was provided, then accumulator will be equal to the first value in the array and currentValue will be equal to the second.

```JavaScript
var desks = [
  { type: 'sitting' },
  { type: 'standing' },
  { type: 'sitting' },
  { type: 'sitting' },
  { type: 'standing' }
];

var deskTypes = desks.reduce(function(previous, desk) {
   if ( desk.type === 'sitting' ) {
        previous.sitting++;
   }
   if ( desk.type === 'standing' ) {
        previous.standing++;
   }
    return previous;
}, { sitting: 0, standing: 0 });

console.log(deskTypes); // { sitting: 3, standing: 2 }
```

Note: If initialValue isn't provided, reduce will execute the callback function starting at index 1, skipping the first index. If initialValue is provided, it will start at index 0.


```JavaScript
// Write a function called 'unique' that will remove all the duplicate values from an array.

var numbers = [1, 1, 2, 3, 4, 4];

function unique(array) {
  return array.reduce(function(previous, element) {
      if (element !== previous.find(el => el === element)) {
        previous.push(element)
      }
      return previous;
  }, [])
}

console.log(unique(numbers)); // [1, 2, 3, 4]
```

If the array is empty and no initialValue was provided, TypeError would be thrown. If the array has only one element (regardless of position) and no initialValue was provided, or if initialValue is provided but the array is empty, the solo value would be returned without calling callback.

It is usually safer to provide an initial value because there are three possible outputs without initialValue, as shown in the following example.
