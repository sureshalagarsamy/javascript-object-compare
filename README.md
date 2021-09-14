### How to Compare Objects in JavaScript



* Reference check
* Manual compare
* Shallow check
* Deep check

### Reference check
 * strict equality operator `===`
 * loose equality operator `==`
 * `Object.is()` function

```js
let person1 = {
    firstName: 'Suresh',
    lastName: 'Alagarsamy'
}

let person2 = {
    firstName: 'Suresh',
    lastName: 'Alagarsamy'
}

console.log(person1 === person2);   // false
console.log(person1 == person2);   // false
Object.is(person1, person2);   // false
```

### Manual compare

```js
function isPersonEqual(object1, object2) {
    return object1.firstName === object2.firstName;
}

let person1 = {
    firstName: 'A'
}

let person2 = {
    firstName: 'B'
}

let person3 = {
    firstName: 'A'
}

isPersonEqual(person1, person2); // false
isPersonEqual(person1, person3); // true
```

### Shallow check

```js
function shallowCheck(object1, object2) {
    let keys1 = Object.keys(object1);
    let keys2 = Object.keys(object2);
    if(keys1.length !== keys2.length)
        return false;
    for(let key of keys1) {
        if(object1[key] !== object2[key]) 
            return false;
    }
    return true;
}

let person1 = {
    firstName: 'A',
    lastName: 'B'
}

let person2 = {
    firstName: 'A',
    lastName: 'B'
}

let person3 = {
    firstName: 'A'
}

shallowCheck(person1, person2); // true
shallowCheck(person1, person3); // false
```

##### Shallow check for nested objects

```js
function shallowCheck(object1, object2) {
    let keys1 = Object.keys(object1);
    let keys2 = Object.keys(object2);
    if(keys1.length !== keys2.length)
        return false;
    for(let key of keys1) {
        if(object1[key] !== object2[key]) 
            return false;
    }
    return true;
}

let person1 = {
    firstName: 'A',
    address: {
        city: 'Bangalore'
    }
}

let person2 = {
    firstName: 'A',
    address: {
        city: 'Bangalore'
    }
}

let person3 = {
    firstName: 'A'
}

shallowCheck(person1, person2);
```

This time, even both `person1` and `person2` having the same content, `shallowCheck(person1, person2)` returns `false`.

The nested objects `person1.address` and `person2.address` are different object instances. 

Thus the shallow equality considers that `person1.address` and `person1.address` are different values.
