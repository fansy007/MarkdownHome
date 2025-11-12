# data types
Number
String
Boolean
Undefined
Null
Symbol
BigInt

dynamic type, when define a varible, no need determine data type at once

# declare 变量
let -- means the value we can change lator
const -- define a value can not be changed, and you should give a const a value immediately when you define it
var -- we can avoid use this, it's old way

# Functions
```javascript
'use strict'
function fruiteMaker(apples,oranges) {
    const juice = `juice with ${apples} apples and ${oranges} oranges`;
    return juice;    
}

const sum = function(a,b) {
    return a+b;
}
console.log(sum(10,20));
```

## lamda function
```javascript
const sum2 = (a,b) => {
    return a+b;
}
console.log(sum2(10,20));
```

lamda function can't get a this scope

## use function as a param
```javascript
function fruiteMaker(apples, oranges,fun) {
    const juice = `juice with ${fun(apples)} apples pieces and ${fun(oranges)} oranges pieces`;
    return juice;
}

const cutFruitPieces = fruit => fruit * 4
const cutFruitPieces2 = fruit => fruit * 10

console.log(fruiteMaker(4,5,cutFruitPieces));
console.log(fruiteMaker(4,5,cutFruitPieces2));

```

 # Array
 ```javascript
const friends = ['Tom','Jack'];
const frieds2 = new Array("Lisa","Mary");
console.log(friends,frieds2);
```

```javascript
const friends = ['Tom','Jack'];
friends.push('Jay');
friends.unshift('Johnson');

// pop() -- pop last element, shift() pop first element
log(friends);
log(friends.indexOf('Tom'));
log(friends.includes('Jay'));
```

# Object
```javascript
const jonas = {
    fisstName: 'Jonas',
    lastName: 'Schmedtman',
    age: 2037-1991,
    job: 'teacher',
    friends: ['Micheal','Peter', 'Steven']
}
log(jonas['friends'][2]); // equals jonas.friends[2]
const nameKey ='lastName';
log(jonas[nameKey]);
```
