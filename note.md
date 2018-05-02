# work notes

## 1. 工作账号 s

公司代码库：GitLab A: `sai.lu@itdev.xiangguang.com` , P：`12345678`

公司电脑：登录本地 **Administrator： `.\Administrator`, P: `!QAZ1qaz`**

公司电脑自己搞的 teamcity:
teamCity： `admin 123456`,
super token： `admin`

---

## 2. npm 淘宝镜像使用方法(三种办法任意一种都能解决问题，建议使用第三种，将配置写死，下次用的时候配置还在)

> 1.通过 config 命令

```bash
.1 npm config set registry https://registry.npm.taobao.org
.2 npm info underscore

#（如果上面配置正确, 2 会有字符串response）
```

> 2.命令行指定

```bash
npm --registry https://registry.npm.taobao.org info underscore
```

> 3.编辑 ~/.npmrc 加入下面内容

```config
registry = https://registry.npm.taobao.org
```

---

## 4. 建立或使用镜像,参考: <https://github.com/cnpm/cnpmjs.org>

## 5. 优化图片方法：在适宜时提供 svg，否则`webP`图片，`picaxal 图像加载库`，缓存

## 6. 安装 chromedriver 失败解决方法

```bash
npm install --save-dev chromedriver --chromedriver_cdnurl=http://cdn.npm.taobao.org/dist/chromedriver
```

---

## 7. knockoutjs 方便调试

```html
<span data-bind="text: ko.toJSON(commodityItem)"></span>
```

---

## 8. JetBrain 激活服务器 <http://idea.codebeta.cn>

---

## 9. `fiddler`, `Vorlon.js`、 `Weinre` 等用于移动端浏览器的远程调试工具。

---

## 10. 从 Windows 路径 获取文件 名字

```JavaScript
var b = String.raw`C:\Funds-Backend\UploadFiles\PaymentApply\94524f3b-7e32-4349-942f-88d8393b4035.png`.split('\\');

var c = b.slice(2).join('/');

console.log(c);
```

---

## 11. 区块链相关技术：智慧合约，编程，密码学【hash 算法，数字指纹, etc】

---

## 12. chrome: CMD+Shift+P, capture full size screenshot, 截图

---

## 13. wifidot: nohup npm start & , 运行

---

## 14. 去掉 input type 为 number 时，上下滚动箭头

```CSS
    input[type='number'] {
        -moz-appearance:textfield;
    }

    input::-webkit-outer-spin-button,
    input::-webkit-inner-spin-button {
        -webkit-appearance: none;
        margin: 0;
    }
```

---

## 15. Vuejs, 数据多的时候可以 freeze 改善性能

```JavaScript
this.item = Object.freeze(Object.assign({}, this.item, changedFields))
```

---

## 16. FP -> Currying of `sum` method

```JavaScript
function sum() {
    var s = Array.prototype.reduce.call(arguments, function (x, y) { return x + y; }, 0);
    var f = function () {
        var a = Array.prototype.slice.call(arguments);
        a.push(s);
        return sum.apply(null, a);
    };
    f.valueOf = function () { return s; };
    return f;
}

sum(1,2,3,4);
sum(1)(2)(3);
sum(1,2)(3);
```

---

## 17. Recursion 递归 Ex

```JavaScript
// Ex 1:
let countDownFrom = (num) => {
    if (num === 0) return
    console.log(num)
    countDownFrom(num -1)
};

countDownFrom(10);

// Ex 2:
let categories = [
    { id: 'animals', 'parent': null },
    { id: 'mammals', 'parent': 'animals' },
    { id: 'cats', 'parent': 'mammals' },
    { id: 'dogs', 'parent': 'mammals' },
    { id: 'chihuahua', 'parent': 'dogs' },
    { id: 'labrador', 'parent': 'dogs' },
    { id: 'persian', 'parent': 'cats' },
    { id: 'siamese', 'parent': 'cats' }
]

let makeTree = (categories, parent) => {
    let node = {}
    categories
    .filter(c => c.parent === parent)
    .forEach(c => node[c.id] = makeTree(categories, c.id))
    return node
}

console.log(
    JSON.stringify(
        makeTree(categories, null))
    , null, 2);

// Ex 3
function getNestedChildren(arr, parent) {
    var out = []
    for(var i in arr) {
        if(arr[i].parent == parent) {
            var children = getNestedChildren(arr, arr[i].id)

            if(children.length) {
                arr[i].children = children
            }
            out.push(arr[i])
        }
    }
    return out
}

const dataa = [
    {id: 1, title: 'hello', parent: 0},
    {id: 2, title: 'hello', parent: 0},
    {id: 3, title: 'hello', parent: 1},
    {id: 4, title: 'hello', parent: 3},
    {id: 5, title: 'hello', parent: 4},
    {id: 6, title: 'hello', parent: 4},
    {id: 7, title: 'hello', parent: 3},
    {id: 8, title: 'hello', parent: 2}
];

getNestedChildren(data, 0);
```

---

## 18 Test CodePen Embed Code Snippet

```HTML
<p data-height="265" data-theme-id="0" data-slug-hash="deyOEB" data-default-tab="js,result" data-user="ellipse" data-embed-version="2" data-pen-title="deyOEB" class="codepen">See the Pen <a href="https://codepen.io/ellipse/pen/deyOEB/">deyOEB</a> by Lusai (<a href="https://codepen.io/ellipse">@ellipse</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>
```

---

## 19 check obj is `Array`

```JavaScript
// 1 fail with iframe
obj.instanceof Array

// 2 fail with iframe
obj.constructor === Array

// 3 rely on Object.prototype.toString and call method
Object.prototype.toString.call(obj) === '[object Array]'

// 4 ES5  the best
if (Array.isArray) {
    return Array.isArray(v);
}

//Polyfill
if(!Array.isArray) {
    Array.isArray = function(arg) {
        return Object.prototype.toString.call(arg) === '[object Array]';
    }
}

// 5 the fatest way and all browsers supported
function isArray(value){
    return value && typeof value === 'object' && value.constructor === Array;
}
```

---

## 20. check is `string`

```JavaScript
function isString(value) {
    return typeof value === 'string' || value instanceof String;
}
```

---

## 21. check is `function`

```JavaScirpt
function isFunction (value) {
    return typeof value === 'function';
}
```

---

## 22. check is `Null & undefined`

```JavaScirpt
function isNull (value) {
    return value === null;
}

function isUndefined (value) {
    return typeof value === 'undefined';
}
```

---

## 23. check is `Boolean`

```JavaScirpt
function isBoolean (value) {
    return typeof value === 'boolean';
}
```

---

## 24. check is `RegExp`

```JavaScirpt
function isRegExp (value) {
    return value && typeof value === 'object' && value.constructor === RegExp;
}
```

---

## 25. check is `Error`

```JavaScirpt
function isError (value) {
    return value instanceof Error && typeof value.message !== 'undefined';
}
```

---

## 26. check is `Date`

```JavaScirpt
function isDate (value) {
    return value instanceof Date;
}
```

---

## 27. check is `Symbol`

```JavaScirpt
function isSymbol (value) {
    return typeof value === 'symbol';
}
```

---

## 28. check is `Error`

```JavaScirpt
function isError (value) {
    return value instanceof Error && typeof value.message !== 'undefined';
}
```

---

## 29. Axios Cancel Request

> for example, in Vuejs

```JavaScript
// declare the cancel function
let cancel

export default {
    ...
    methods: {
        query() {
            axios.get(`${url}`, {
                params: {},
                cancelToken: new axios.CancelToken(function (c) {
                    cancel = c
                })
            })
            .then(response => {
                ...
            })
            .catch(error => {
                // catch the `cancel` message
                if (axios.isCancel(error)) {
                    console.log(error)
                    alert('xxx')
                } else {
                   console.log(error)
                }
            })
        },

        someFunc () {
            // call the `cancel` function
            cancel('you have cancel the request')
        }
    }
}
```

---

## 30. Array Deduplication

```js
//without indexof...
let uniqueWithoutArrayMethod = arr => {
  let res = [arr[0]];
  for (let i = 1; i < arr.length; i++) {
    let repeat = false;
    for (let j = 0; j < res.length; j++) {
      if (arr[i] === res[j]) {
        repeat = true;
        break;
      }
    }
    if (!repeat) {
      res.push(arr[i]);
    }
  }
  return res;
};
console.log(uniqueWithoutArrayMethod([1, 1, 2, 3, 5, 3, 1, 5, 6, 7, 4, 3]));

// with another array
let uniqueWithAnotherArray = arr => {
  let result = [];
  let len = arr.length;
  for (let i = 0; i < len; i++) {
    // if (result.indexOf(arr[i]) < 0) {
    if (!result.includes(arr[i])) {
      result.push(arr[i]);
    }
  }
  return result;
};
console.log(uniqueWithAnotherArray([1, 1, 2, 3, 5, 3, 1, 5, 6, 7, 4, 3]));

//with Object
let uniqueWithOject = arr => {
  let obj = {};
  arr.map(a => (obj[a] = a));
  let result = Object.values(obj);
  return result;
};
console.log(uniqueWithOject([1, 1, 2, 3, 5, 3, 1, 5, 6, 7, 4, 3]));

//with set
let uniqueWithSet = arr => {
  let arr3 = [...new Set(arr)];
  let arr5 = Array.from(new Set(arr));
  return arr3;
};
console.log(uniqueWithSet([1, 1, 2, 3, 5, 3, 1, 5, 6, 7, 4, 3]));

//deduplication on self，change origin array
let uniqueOnSelf = arr => {
  let len = arr.length;
  for (let i = 0; i < len; i++) {
    for (let j = i + 1; j < len; j++) {
      if (arr[j] === arr[i]) {
        arr.splice(j, 1);
        j--;
        len--;
      }
    }
  }
  return arr;
};
console.log(uniqueOnSelf([1, 1, 2, 3, 5, 3, 1, 5, 6, 7, 4, 3]));
```

---

## 31. 金额格式化

```JavaScript
  Number.prototype.toCurrencyString = function(prefix, suffix) {
    if (typeof prefix === 'undefined') { prefix = '$'; }
    if (typeof suffix === 'undefined') { suffix = ''; }
    var _localeBug = new RegExp((1).toLocaleString().replace(/^1/, '').replace(/\./, '\\.') + "$");
    return prefix + (~~this).toLocaleString().replace(_localeBug, '') + (this % 1).toFixed(2).toLocaleString().replace(/^[+-]?0+/,'') + suffix;
  }

  var MyNumber = 123456789.125;
  console.log(MyNumber.toCurrencyString());
```

---

## 32 lodash 合并对象

```js
function customizer(objValue, srcValue) {
  if (_.isArray(objValue)) {
    if (objValue[0] !== srcValue[0]) {
      return objValue.concat(srcValue);
    } else {
      return objValue;
    }
  }
}

var object = { a: [1], b: [2] };
var other = { a: [1], b: [4] };

// output: {a: [1], b: [2, 4]}
_.mergeWith(object, other, customizer);
```

---

## 33. Abort `fetch` request. [AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController)

```html

<div>
    <button class="download">fetch</button>
    <button class="abort">cancel fetch</button>
</div>

```

```js

//ex
var controller = new AbortController();
var signal = controller.signal;

var downloadBtn = document.querySelector('.download');
var abortBtn = document.querySelector('.abort');

downloadBtn.addEventListener('click', fetchData);

abortBtn.addEventListener('click', function() {
    controller.abort();
    console.log('fetch data cancel or aborted...');
});

function fetchData() {
    fetch('https://api.github.com/users/dddd', { signal }).then(function(response) {
        console.log(response);
    }).catch(function(e) {
        console.log('get data error: ' + e.message);
    })
}

```

> Note: When `abort()` is called, the `fetch()` promise rejects with an `AbortError`

---

## 34.