# learning-diary

### 20.10.22
Write a publishDateForDisplay function. Its job is to return the publish date for a blog post, formatted as a string, wrapped in a promise. We've provided a formatDate function, so you won't need to call any methods on the date objects.

publishDateForDisplay takes a date wrapped in a promise, like Promise.resolve(publishDate). If the date is undefined, it should return the string 'unpublished'. Otherwise it should return the result of formatDate(publishDate).

```
function formatDate(date) {
  // Turn the date object into a string like '2024-11-19'
  return [date.getFullYear(), date.getMonth() + 1, date.getDate()]
    .join('-');
 }

function publishDateForDisplay(publishDatePromise) {
  return publishDatePromise.then(publishDate => {
    if (publishDate === undefined) {
      return 'unpublished';
    } else {
      return formatDate(publishDate);
    }
  });
 }

// Format one actual date and one undefined date.
const date1 = new Date('November 19, 2024 00:00:00');
const date2 = undefined;
publishDateForDisplay(Promise.resolve(date1)).then(formatted1 =>
  publishDateForDisplay(Promise.resolve(date2)).then(formatted2 =>
    [formatted1, formatted2]
  )
 );

{fulfilled: ['2024-11-19', 'unpublished']}
```

### 23.10.22
```
const array = []
array.push(‘before’);

const promise1 = Promise.resolve(‘this value is ignored’);
const promise2 = promise1.then(() => {
	array.push(‘then’);
});

promise2.then(() => {
	array.push(‘after’);
	return array;
});
```

```
Function findUser(id) {
	const = users.find( u => u.id === id);
if (user === undefined) {
	return Promise.reject(new Error(‘user does not exist’));
} else {
return user;
}
```
### 24.10.22
Catching promises
```
Promise.catch(reason =>  {
    throw new Error(reason.message)
  });
```

```
let savedResolve;

const promise = new Promise(resolve => { savedResolve = resolve; });

/* The `savedResolve` variable now contains the function that we got from the
 * `new Promise` constructor. Calling it will fulfill the promise, even
 * though it now looks like "savedResolve" and "promise" are unrelated. */
savedResolve(3);

promise;
```
### 29.10.22
Assigning a promise constructor's resolve function to a variable.

```
let savedResolve;
const promise = new Promise(resolve => { savedResolve = reslove; });
savedResolve(5);
promise;
```

This code's rejection reason is an object with a message property. Add a catch to catch the rejection, then re-throw a proper Error that contains the message.

```
const promise = Promise.reject({message: 'it failed'});
promise.catch(reason => {throw new Error(reason.message);
});

fulfilledValues function takes a promises array as an argument and returns an array of the fulfilled values from the promises. Rejected promises are ignored, since they don't have a fulfilled value.

function fulfilledValues(promises) {
  return Promise.allSettled(promises).then(results => {
  return results
    .filter(result => result.status === 'fulfilled'
    .map(result => result.value);
    });
}

fulfilledValues([
  Promise.resolve('Amir'),
  Promise.reject(new Error("User doesn't exist")),
  Promise.resolve('Cindy'),
]);
{fulfilled: ['Amir', 'Cindy']}
```

### 30.10.22

sleep(ms) function. This function uses the promise constructor (new Promise) to return a promise that resolves after the specified number of milliseconds. Inside the promise, setTimeout delays calling the resolve function.

```
function sleep(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
```

### 04.11.22

There are two isNaNs and that one of them is preferable
Preferred:

```
Number.isNaN(undefined);
// false
```
A design mistake in Javascript:

```
> isNaN(undefined);
// true
```

### 10.11.22

Function that takes a user and returns a login count object for this user, mapping their name to their loginCount. Uses a computed property to construct the object.

```
const users = [
  {name: 'Amir', loginCount: 5},
  {name: 'Betty', loginCount: 16},
];

function loginCount(user) {
	return {[user.name]: user.loginCount};
}

[
  loginCount(users[0]),
  loginCount(users[1]),
];
```


### 13.11.22

#### Sets
Using large sets is quicker and more efficient than using large arrays. Sets can be used to check if an array has duplicates. These two functions uses a set to decide whether an array of numbers has any duplicates. It returns true if there are duplicates; otherwise it return falses.

```
function hasDuplicates(numbers) {
  return (new Set(numbers)).size !== numbers.length;
}
```
```
function hasDuplicates(numbers) {
	const set = new Set();
	for (const n of numbers) {
		if (set.has(n)) {
			return true;
			}
			set.add(n);
		}
		return false;
	}
```
#### Safe Integers
```
function safeIntegerMultiply(x, y) {
  let array = []
  let check =x*y;
  if (Number.isSafeInteger(check) === true) {
    return check;
  }
  else {
    throw new Error('Product is an unsafe integer')
  }
}
```
Does the same as:

```
function safeIntegerMultiply(x, y) {
	const product = x * y;
	if (!Number.isSafeInteger(product)) {
		throw new Error('Product is an unsafe integer');
	}
	return product;
}
```

### 14.11.22

#### Extending classes

Class that inherits from User. Its constructor calls super, passing along the relevant arguments. It also sets the admin's isAdmin flag to true

```
class User {
  constructor(name, email) {
    this.name = name;
    this.email = email;
    this.isAdmin = false;
  }
}

class Admin extends User {
   constructor(name, email, isAdmin) {
    super(name, email, isAdmin);
      this.isAdmin = true;
  }
}

const admin = new Admin('Amir', 'amir@example.com');
[admin.name, admin.email, admin.isAdmin];
```
### 16/11/22

#### Defer
The defer attribute is a boolean attribute. If the defer attribute is set, it specifies that the script is downloaded in parallel to parsing the page, and executed after the page has finished parsing.

There are several ways an external script can be executed:
- If async is present: The script is downloaded in parallel to parsing the page, and executed as soon as it is available (before parsing completes)
- If defer is present (and not async): The script is downloaded in parallel to parsing the page, and executed after the page has finished parsing
- If neither async or defer is present: The script is downloaded and executed immediately, blocking parsing until the script is completed

#### Anonymous and inline classes
Defines an anonymous rectangle class inside of an array. Constructor takes width and height arguments and has an area method that returns the rectangle's area (the width times the height). 

```
const classes = [
	class {
		constructor(width, height) {
		this.width = width;
		this.height = height;
		}
		
		area() {
		return this.width * this.height;
		}
	}
];

const Rectangle = classes[0];
const rectangle = new Rectangle(3,4);
[rectangle.area(), classes[0].name];
```

#### Accessor properties on classes

```
class User {
  constructor(name) {
     this.names = [name];
  }
  
  set name(newName) {
    this.names.push(newName);
  }
}
  
const user = new User('Amir');
const names1 = user.names.slice();
user.name = 'Betty';
const names2 = user.names.slice();
({names1, names2});
}

returns 
{names1: ['Amir'], names2: ['Amir', 'Betty']}
```

### 18/11/22

#### Set unions
General purpose function to unite sets.

```
function setUnion(setA, setB) {
	return new Set([...setA,...set`B]);
}
```
General purpose function to find intersection of sets.
```
function setIntersection(set1, set2) {
  return new Set(
  Array.from(set1).filter(n => set2.has(n))
);
}
```

## 26/12/22

```
class SocialGraph {
  constructor() {
    this.map = new Map();
  }

  addFollow(user1, user2) {
    if (!this.map.has(user2)) {
      this.map.set(user2, []);
    }
    this.map.get(user2).push(user1);
  }

  follows(user1, user2) {
    if (this.map.has(user2)) {
      return this.map.get(user2).includes(user1);
    }
  return false;
  }
}

const socialGraph = new SocialGraph();
socialGraph.addFollow('amir', 'betty');
socialGraph.addFollow('amir', 'cindy');
socialGraph.addFollow('betty', 'cindy');

[
  socialGraph.follows('amir', 'betty'),
  socialGraph.follows('amir', 'cindy'),
  socialGraph.follows('betty', 'amir'),
  socialGraph.follows('betty', 'cindy'),
  socialGraph.follows('cindy', 'amir'),
  socialGraph.follows('cindy', 'betty'),
];


[true, true, false, true, false, false]
```

