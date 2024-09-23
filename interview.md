# 前端面试

## JavaScript

### js 对象及数组的常用函数

```js
const a = [1, 2, 3, 4, 5];
// Implement this
a.multiply();
console.log(a); // [1, 2, 3, 4, 5, 1, 4, 9, 16, 25]
```

> 以下输出结果是:

```js
for (var i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i);
  }, 100 * i);
}
```

> array deduplicate

```js
const array = [1, 2, 3, 41, 1, 3, 55]

// 1 using Set
[...new Set(array)]

// 2 using filter
array.filter((item, index) => array.indexOf(item) === index)

// 3 using reduce
array.reduce((unique, item) => unique.includes(item) ? unique : [...unique, item], [])

```

---

### Following code returns `false` in JavaScript. Justify why it happens

```js
// false
0.2 + 0.1 === 0.3;
```

---

### why `b` become a global variable when call this function

```js
function myFunc() {
  let a = b = 0;
}

myFunc();

// because it equals to above code:
function myFunc() {
  let a = (b = 0);
}

myFunc();

// how to solve this problem
function myFunc() {
  let a,b;
  a = b = 0;
}
myFunc();
```

---

### tiny function

````js
function printing() {
  console.log(1);
  setTimeout(function() {
    console.log(2);
  }, 1000);
  setTimeout(function() {
    console.log(3);
  }, 0);
  console.log(4);
}
// 1 4 3 2

////////////////////
function* g1() {
  yield 2;
  yield 3;
  yield 4;
}

function* g2() {
  yield 1;
  yield* g1();
  yield 5;
}

var iterator = g2();
console.log(iterator);

////////////////////

// FP
function sum() {
  var s = Array.prototype.reduce.call(
    arguments,
    function(x, y) {
      return x + y;
    },
    0
  );
  var f = function() {
    var a = Array.prototype.slice.call(arguments);
    a.push(s);
    return sum.apply(null, a);
  };
  f.valueOf = function() {
    return s;
  };
  return f;
}

sum(1, 2, 3, 4);
sum(1)(2)(3);
sum(1, 2)(3);

//////////////////

// Cloure && EventLoop
for (var i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i);
  }, 100 * i);
}

//for(var i = 0; i< 10; i++){
// setTimeout((function() {
// console.log(i)
// })(i), 100*i)
//}

// for(let i = 0; i< 10; i++){
// setTimeout(function() {
// console.log(i)
//}, 100*i)
//}

---

### Ask `iterator`

```js
// Don't change code, let it run
const [a, b] = {
	a: 11,
	b: 22
}
console.log(a,b)
```

> Answer: Using `Symbol.iterator`

```
Object.prototype[Symbol.iterator] = function () {
	return Object.values(this)[Symbol.iterator]()
}

// or using generator
Object.prototype[Symbol.iterator] = function* () {
	yield Object.value(this)
}
```

---

### js 对象深浅拷贝

### Macrotasks and Microtasks diff

```js
/** What will be the output of this code? 
 * result: 1 7 3 5 2 6 4 
 * why?
*/

console.log(1);

setTimeout(() => console.log(2));

Promise.resolve().then(() => console.log(3));

Promise.resolve().then(() => setTimeout(() => console.log(4)));

Promise.resolve().then(() => console.log(5));

setTimeout(() => console.log(6));

console.log(7);
```

---

### Implement a simple data binding using JavaScript Proxy

Hint: ES Proxy allows you to intercept a call to any object property or method. To start with, DOM should be updated whenever an underlying bound object is changed.

---

### Explain JavaScript concurrency model

Hint: Look for Event loop, task queue, call stack, heap, etc.

---

### What are the different function invocation patterns in JavaScript? Explain in detail.

Hint: There are four patterns, function call, method call, .call() and .apply().

---

### Explain any new upcoming ECMAScript proposal.

Hint: As in 2018, `BigInt`, `partial function`, `pipeline operator`, etc.

---

### If we convert the following object to JSON string, what would happen

```js
const a = {
    key1: Symbol(),
    key2: 10
}
// What will happen
console.log(JSON.stringify(a));
````

---

### Are you familiar with Typed Arrays? If yes, explain their need and differences as compared to traditional arrays in JavaScript

---

### AMD, CMD, CommonJS, UMD

---

## HTML & CSS

### What is the use of Doctype in HTML

Specifically what will happen in each of the following scenarios:

- Doctype is absent.
- HTML4 Doctype is used but HTML page uses HTML5 tags like <audio> or <video>. Will it cause any error?
- Invalid Doctype is used.

---

### css flexbox grid

---

### How CSS pixel is different than hardware/physical pixel

Hint: A pixel is not a pixel is not a pixel — ppk.

---

### What's the difference between the in operator and the hasOwnProperty method in objects?

> As you know both of these features check if a property exists in an object. It will return truefalse. The difference between them is that the `in` operator also checks the objects' `Prototype Chain` if the property was not found in the current object while the hasOwnProperty method just checks if the property exists in the `current object` ignoring the `Prototype Chain`.

---

## Vue

### List some features of Vue.js

> Vue js comes with following features

- Virtual DOM 深入些问下 dom-diff 算法
- Templates
- Reactivity
- Components 深入 Web-Components
- Transitions
- Routing
- Light weight VueJS is light weight library compared to other frameworks

---

### Vue instance lifecycle

<img width="100" src="https://vuejs.org/images/lifecycle.png" alt="Vue lifecycle" />

---

### What is the difference v-bind and v-model? Provide some code example

```html
<input v-model="something" />

<!-- it's just syntactic sugar for: -->
<input v-bind:value="something" v-on:input="something = $event.target.value" />
```

---

### vue cli 原理

---

### vue-router

> router order: what's the difference of below code snippet?

```js
const routeA = new VueRouter({
  routes: [
    {
      path: "/user/:userId",
      component: PageUser
    },
    {
      path: "/user/me",
      component: PageMe
    }
  ]
});

const routeB = new VueRouter({
  routes: [
    {
      path: "/user/me",
      component: PageMe
    },
    {
      path: "/user/:userId",
      component: PageUser
    }
  ]
});
```

---

### v-if v-show 区别

---

### Change Detection Caveats

Due to the limitations of modern JavaScript (and the abandonment of Object.observe), Vue cannot detect property addition or deletion.

```js
// Object
this.$set(this.someObject, 'b', 2)

Vue.set(vm.someObject, 'b', 2)

this.someObject = Object.assign({}, this.someObject, { a: 1, b: 2 })

// Array
> Due to limitations in JavaScript, Vue cannot detect the following changes to an array:

- When you directly set an item with the index, e.g. vm.items[indexOfItem] = newValue
- When you modify the length of the array, e.g. vm.items.length = newLength

vm.$set(vm.items, indexOfItem, newValue)
vm.items.splice(newLength)
```

---

### Mixins

> Mixins are a flexible way to distribute reusable functionalities for Vue components. A mixin object can contain any component options. When a component uses a mixin, all options in the mixin will be “mixed” into the component’s own options.

---

### Vue 里面 实现 Angular `Service` 的方式 (会 Angular 的可以问下)

- Stateless service: use mixins
- Statefull service: use Vuex
- Export service and import from a vue code
- any javascript global object

---

### Vuex

介绍下 Vuex，及解决了什么问题

- Multiple views may depend on the same piece of state. Passing props can be tedious for deeply nested components, and simply doesn't work for sibling components

- Actions from different views may need to mutate the same piece of state. We often find ourselves resorting to solutions such as reaching for direct parent/child instance references or trying to mutate and synchronize multiple copies of the state via events. Both of these patterns are brittle and quickly lead to unmaintainable code

### 组件嵌套较深，组件间通信问题

> event hub, mixin, vuex, DI

### Computed 和 Watcher

### JSX 使用场景

### SSR

### TypeScript

### Vue3.0 计划

### [70-javascript-interview-questiones](https://dev.to/macmacky/70-javascript-interview-questions-5gfi)
