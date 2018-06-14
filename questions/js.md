# JavaScript

Which version is better? Why?

```js
let animals = ['cats', 'dogs'];
let catsOnly = [];
for (let i = 0; i < animals.length; i++) {
  if (animals[i] === 'cats') {
    catsOnly.push(animals[i]);
  }
}
```

```js
let animals = ['cats', 'dogs'];
let catsOnly = animals.filter(group => group === 'cats');
```

***

Which JS Array method would you use to improve this code (forEach/filter/map/reduce)?

```js
let numbers = [1, 2, 3];
let sum = 0;
for (let i = 0; i < numbers.length; i++) {
  sum += numbers[i];
}
```

***

What will be printed? Why?

```js
console.log('Hello');
setTimeout(() => {
  console.log('Beautiful');
}, 0);
console.log('World');
```

***

Which version is better? Why?

```html
<h1>Students</h1>
<ul>
  <li>Moshe</li>
  <li>Itzik</li>
  <li>Suliman</li>
  <li>Alex</li>
</ul>
```

```js
document.querySelector('ul').addEventListener('click', e => {
  console.log(`You clicked on ${e.target.textContent}`);
});
```

```js
document.querySelector('li').addEventListener('click', e => {
  console.log(`You clicked on ${e.target.textContent}`);
});
```

***

Which function will be easier to test? Why?

```js
let state = 42;
let result;

function doesSomething() {
  if (state > 41) {
    result = true;
  } else {
    result = false;
  }
}
```

```js
function doesSomething(state) {
  return state > 41;
}
```

***

What will be printed? Why?

```js
let dog = {
  name: 'Toby',
  bark: function() {
    console.log(`Woof, ${this.name}!`);
  }
}

let bark = dog.bark;
bark();
```

***

What will be printed? Why?

```js
let dog = {
  bark: function() {
    console.log(`Woof, ${this.name}!`);
  }
}

let toby = Object.create(dog);
toby.name = 'Toby';
toby.bark();
console.log(toby.hasOwnProperty('bark'));
console.log('bark' in Object.getPrototypeOf(toby));
```