# work notes

```js
// TODO replace this code with something better
```

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

const data = [
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
  fetch('https://api.github.com/users/dddd', { signal })
    .then(function(response) {
      console.log(response);
    })
    .catch(function(e) {
      console.log('get data error: ' + e.message);
    });
}
```

> Note: When `abort()` is called, the `fetch()` promise rejects with an `AbortError`

---

## 34. 生成器函数可以用 `GeneratorFunction` 或 `function* expression` 定义。[Link](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/function*)

> 生成器在执行时能暂停，后面又可以从暂停出继续执行。调用一个生成器函数不会立刻执行里面的语句，而是返回一个这个生成器的迭代器(iterator)对象。当这个迭代器的`next()`被首次调用时，其内语句会执行到`yield`的位置为止，`yield`后紧跟迭代器要返回的值。或者如果用的是`yield*`，则表示讲执行权移交给另外一个生成器函数，当前的生成器暂停执行。
> `next()`方法返回一个对象`{value: '', done: ''}`，`value`为本次`yield`表达式的返回值，`done`属性为布尔类型，表示生成器后续是否还有`yield`语句，即生成器函数是否已经执行完毕并返回。调用`next()`方法时，如果传入了参数，name 这个参数会作为上一条执行的`yield`语句的返回值。

```js
/* Generator */

function* iterArray(arr) {
  if (Array.isArray(arr)) {
    for (let i = 0; i < arr.length; i++) {
      yield* iterArray(arr[i]);
    }
  } else {
    yield arr;
  }
}

// for-of
var arr = ['a', ['b', 'c'], ['d', 'e', 'f']];

for (var x of iterArray(arr)) {
  console.log(x);
}

// 迭代器展开
var gen = iterArray(arr);
arr = [...gen];
console.log(arr);
```

---

## 35. 怪异模式[MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)

---

## 36. 可视化库 [Blog](https://thenextweb.com/dd/2015/06/12/20-best-javascript-chart-libraries/)

---

## 37. 导出 csv [参考链接](https://stackoverflow.com/questions/14964035/how-to-export-javascript-array-info-to-csv-on-client-side)

[参考 2](https://stackoverflow.com/questions/18848860/javascript-array-to-csv/18849208#18849208)

```js
// Assuming you are using an array of arrays for your data
const rows = [
  ['name1', 'city1', 'some other info'],
  ['name2', 'city2', 'more info']
];

const dataToCsvURI = data =>
  encodeURI(
    `data:text/csv;charset=utf-8,${data
      .map((row, index) => row.join(','))
      .join(`\n`)}`
  );

const link = document.createElement('a');

link.setAttribute('href', dataToCsvURI(rows));

link.setAttribute('download', 'my_data.csv');

link.innerHTML = 'Click Here to download';

document.body.appendChild(link);

link.click();
```

```js
function downloadableCSV(rows) {
  var content = 'data:text/csv;charset=utf-8,';

  rows.forEach(function(row, index) {
    content += row.join(',') + '\n';
  });

  return encodeURI(content);
}

var rows = [
  ['name1', 2, 3],
  ['name2', 4, 5],
  ['name3', 6, 7],
  ['name4', 8, 9],
  ['name5', 10, 11]
];

$('#download').click(function() {
  window.open(downloadableCSV(rows));
});
```

---

## 38 `Reactive programming` [Good Post](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754)

> Reactive programming is programming with asynchronous data streams.

## 39. Download file from server when response is `blob` data

```js
downloadFile (fileName, blob) {
    let url = URL.createObjectURL(blob)
    let a = document.createElement('a')
    a.download = fileName
    a.href = url
    a.click()
}

downloadFTPFile (params) {
    const { fileName, filePath } = { ...params.row }
    if (fileName && filePath) {
      axios.post(`ftp/download`, null, {
        params: {
          fileName,
          filePath
        },
        responseType: 'blob' // important!!!
      })
        .then(res => {
          // const disposition = res.request.getResponseHeader(
          //   "Content-disposition"
          // )
          // const fileName = decodeURI(disposition.split("filename=")[1])
          let resBlob = res.data
          // different type, has two methods.
          // 1.
          let url = window.URL.createObjectURL(new Blob([resBlob], {
            'type': 'application/octet-stream'
          }))
          // 2.
          // let url = window.URL.createObjectURL(resBlob)
          let a = document.createElement("a")
          a.download = fileName
          a.href = url
          a.click()
          this.$Message.success('下载成功')
        })
```

---

## 40. `performance` API

```js
performance
  .getEntriesByType('resource')
  .map(t => t.name)
  .filter(url => url.includes('woff'))
  .join('\n');
```

---

## 41. chrome devTools new func, [u2 link](https://www.youtube.com/watch?v=mfuE53x4b3k&t=0s&index=33&list=PLOU2XLYxmsIInFRc3M44HUTQc3b_YJ4-Y), more about: [Reference](https://developers.google.com/web/tools/chrome-devtools/console/command-line-reference)

> `copy()`

```js
copy();

copy($_); // $_ 返回最近表达式的值
```

> `$_` , [Reference](https://developers.google.com/web/tools/chrome-devtools/console/command-line-reference)

```js
2 + 2;
$_;
$0;
$1;
$2;
$3;
$4;
```

---

> `debug()`

```js
const url = 'https://api.github.com/search/repositories';

const a = async () => {
  const res = await fetch(`${url}?q=workbox`);
  const data = await res.json();
  const names = data.items.map(item => item.name);
  console.log(names);
};
debug(a);

a();
```

---

> `monitor()`

```js
monitor(setTimeout);

setTimeout(_ => console.log('pause'), 500);

console.log('first');

unmonitor(setTimeout);
```

---

> `queryObjects()`

```js
class Foo {}
const a = new Foo();
const b = new Foo();
b.prop = 1;

queryObjects(Foo);
```

---

> `Eager Evaluation`

```js
// in the console
/[0-9]{3}-[0-9]{3}-[0-9]{4}/.exec('Call us 555-867-5309! Thanks');
```

---

> `Cmd + Shift + P`, input `undo`/ `right`/ `undoc`

---

```js
[...document.querySelectorAll('a')]
  .map(e => e.innerText.trim())
  .sort()
  .filter(Boolean);
```

---

## 42. Use `window.crypto` to generate random numbers

```js
let arr = new Uint32Array(10);
window.crypto.getRandomValues(arr);
```

---

## 43. 内容多单元格显示问题 css, [reference](http://hackingui.com/front-end/a-pure-css-solution-for-multiline-text-truncation/)

```css
/* styles for '...' */
.block-with-text {
  /* hide text if it more than N lines  */
  overflow: hidden;
  /* for set '...' in absolute position */
  position: relative;
  /* use this value to count block height */
  line-height: 1.2em;
  /* max-height = line-height (1.2) * lines max number (3) */
  max-height: 3.6em;
  /* fix problem when last visible word doesn't adjoin right side  */
  text-align: justify;
  /* place for '...' */
  margin-right: -1em;
  padding-right: 1em;
}
/* create the ... */
.block-with-text:before {
  /* points in the end */
  content: '...';
  /* absolute position */
  position: absolute;
  /* set position to right bottom corner of block */
  right: 0;
  bottom: 0;
}
/* hide ... if we have text, which is less than or equal to max lines */
.block-with-text:after {
  /* points in the end */
  content: '';
  /* absolute position */
  position: absolute;
  /* set position to right bottom corner of text */
  right: 0;
  /* set width and height */
  width: 1em;
  height: 1em;
  margin-top: 0.2em;
  /* bg color = bg color under block */
  background: white;
}
```

## 44. `Object clone` Shallow or Deep. [reference](https://medium.com/@tkssharma/objects-in-javascript-object-assign-deep-copy-64106c9aefab)

```js
let obj = {
  a: 1,
  b: {
    c: 2
  }
};
let newObj = Object.assign({}, obj);
console.log(newObj); // { a: 1, b: { c: 2} }
obj.a = 10;
console.log(obj); // { a: 10, b: { c: 2} }
console.log(newObj); // { a: 1, b: { c: 2} }
newObj.a = 20;
console.log(obj); // { a: 10, b: { c: 2} }
console.log(newObj); // { a: 20, b: { c: 2} }
newObj.b.c = 30;
console.log(obj); // { a: 10, b: { c: 30} }
console.log(newObj); // { a: 20, b: { c: 30} }
// Note: newObj.b.c = 30; Read why.???.

let someObj = {
  a: 2
};
let obj = Object.create(someObj, {
  b: {
    value: 2
  },
  c: {
    value: 3,
    enumerable: true
  }
});
let objCopy = Object.assign({}, obj);
console.log(objCopy); // { c: 3 }
```

---

## 45. Rendering Performance [Reference](https://developers.google.com/web/fundamentals/performance/rendering/avoid-large-complex-layouts-and-layout-thrashing#avoid-forced-synchronous-layouts)

> 布局是浏览器计算各元素几何信息的过程：元素的大小以及在页面中的位置。 根据所用的 CSS、元素的内容或父级元素，每个元素都将有显式或隐含的大小信息。此过程在 Chrome、Opera、Safari 和 Internet Explorer 中称为布局 (Layout)。 在 Firefox 中称为自动重排 (Reflow)，但实际上其过程是一样的。与样式计算相似，布局开销的直接考虑因素如下：1. 需要布局的元素数量。2.这些布局的复杂性。

## 46. chromedriver fail solution

```bash
npm install --save chromedriver --chromedriver_cdnurl=http://cdn.npm.taobao.org/dist/chromedriver
```

---

## 47

```flow
st=>start:开始
e=>end:结束
op=>operation:操作
cond=>condition:确认

st->op->cond
cond(yes)->e
cond(no)->op
```

```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

---

## 48 element all width and height (<https://msdn.microsoft.com/en-us/library/hh781509(VS.85).aspx)>

## 49 check linux version

```bash
uname -a

uname -mrs

lsb_release -a

cat /proc/version

cat /etc/issue

tail /etc/redhat-release
```

---

## 50. Using `fileReader` to preview multipe image

```html
<input type="file" id="browse" onchange="previewFiles()" multiple />
<div id="preview"></div>
```

```js
function previewFiles() {
  var preivew = document.querySelector('#preview');
  var files = document.querySelector('input[type=file]').files;

  function readAndPreview(file) {
    if (/\.(jpg?g|png|gif)$/i.test(file.name)) {
      var reader = new FileReader();

      reader.addEventListener(
        'load',
        function() {
          var image = new Image();
          image.height = 100;
          image.title = file.name;
          image.src = this.result;
          preivew.appendChild(image);
        },
        false
      );

      reader.readAsDataURL(file);
    }
  }

  if (files) {
    [].forEach.call(files, readAndPreview);
  }
}
```

---

## 51. Vuejs 2 行多了省略号显示 fix autoprefix 7.1 bug

```css
.note-content {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  overflow: hidden;
  text-overflow: ellipsis;
  color: rgba(0, 0, 0, 0.87);
  font-size: 14px;
  /*! autoprefixer: off */
  -webkit-box-orient: vertical;
  /*! autoprefixer: on */
}
```

---

## 52. 前端分页(Vuejs)

```js
export default {
  data() {
    return {
      list: [],
      query: {
        currentPage: 1,
        pageSize: 10
      }
    };
  },
  methods: {
    handleSizeChange(val) {
      this.query.pageSize = val;
      this.excelDataPagination();
    },

    handleCurrentChange(val) {
      this.query.currentPage = val;
      this.excelDataPagination();
    },

    excelDataPagination() {
      let currentPage = this.query.currentPage;
      let pageSize = this.query.pageSize;
      --currentPage;
      this.list = this.all.slice(
        currentPage * pageSize,
        (currentPage + 1) * pageSize
      );
    }
  }
};
```

---

## 53. curl 下载文件

> `curl URL -o filename --progress`

Example:

```bash
curl https://unpkg.com/ag-grid-enterprise@18.1.1/dist/ag-grid-enterprise.min.js -o my-ag-grid
.min.js --progress
```

---

## 54. JetBrains External Tools

Ex: chrome google it

-1 selected the "chrome.exe" etc.

-2 add arguments and insert Macro Param: --new-tab "https://google.com/search?q=$SelectedText$" (--new-window, --incognito, arguments of chrome app)

## 55. Rider Error Solutions Collection, work with `VSStudio`

```text
1 .netStandard, Version=2.0.0.0, Culture=neutral, 的引用问题解决
  在csproj文件里面，添加      <Reference Include="netstandard" />

2. 提示如上(12)错误时，打开Rider设置 -> Toolset and Build -> Use MSBUILD version: Latest installed. [Done]
```

---

## 56. Interest console from icloud.com

```js
window.console &&
  console.log(
    '%c\n                                   *********                           \n                             *******       *******                     \n                           ***                    ***                  \n                         **                         **                 \n                *****   **                           ***               \n             ****   *****                              **              \n           **                                           **             \n          *                                              *             \n         **              **                **            *             \n      ****               **        **      **           ******         \n    **                   **        **      **                 ****     \n  ***                              **                            ***   \n  *                                **                              **  \n *                               ****                               *  \n *                                                                  *  \n**                                                                  ** \n*                            **         **                           * \n**                            ***********                            * \n *                                ***                               ** \n  **                                                               **  \n   ***                                                            **   \n      ****                                                     ****    \n         ****                                               ****       \n            *************************************************          \n \n Happy to see you here! We are hiring the sharpest minds in the\n industry who want to build the most sophisticated and delightful\n applications on the web.\n \n Check out https://www.icloud.com/jobs/\n \n',
    'font-family: Menlo, monospace'
  );
```

---

## 57. Intl format `currency`, `locale` etc. [Intl](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl)

> Ex: `Vue` currency filter

```js
export default {
  filters: {
    currency(value) {
      return new Intl.NumberFormat('en-US', {
        style: 'currency',
        currency: 'USD'
      }).format(value);
    }
  }
};
```

> Use

```html
<span>{{value | currency}}</span>
```

> other example

```js
console.log(
  new Intl.NumberFormat('en-IN', {
    style: 'currency',
    currency: 'RMB',
    minimumFractionDigits: 6
  }).format(12345789.23654)
);
```

> format digit

```js
...
filters: {
  currency(value, places) {
    return new Intl.NumberFormat("en-US",
    {
      style: "currency",
      currency: "USD",
      minimumFractionDigits: places || 2,
      maximumFractionDigits: places || 2
    }).format(value)
  }
}
```

---

## 58. XSS `cross site scripting`, where we let someone else run JavaScript on our page.[web bos](https://wesbos.com/sanitize-html-es6-template-strings/)

```js
const first = 'Wes';
const aboutMe = `I love to do evil <img src="http://unsplash.it/100/100?random" onload="alert('you got hacked');" />`;

const html = `
    <h3>${first}</h3>
    <p>${aboutMe}</p>
`;

const bio = document.querySelector('img');
bio.innerHTML = html;
```

> Solution: `Sanitizing` your HTML. Using `DOMPurify` (<https://github.com/cure53/DOMPurify)> library.

```js
<script src="https://cdnjs.cloudflare.com/ajax/libs/dompurify.0.8.2/purify.min.js"></script>
<script>
function sanitize(strings, ...values) {
    const dirty = strings.reduce((prev, next, i) => `${prev}${next}${values[i]} || ''}`, '');
    return DomPurify.sanitize(dirty);
}
const first = 'Wes';
const aboutMe = sanitize`I love to do evil <img src="http://unsplash.it/100/100?random" onload="alert('you got hacked');" />`;

const html = `
    <h3>${first}</h3>
    <p>${aboutMe}</p>
`;

const bio = document.querySelector('.bio');
bio.innerHTML = html;
</script>
```

---

## 59. InteliJ plugins: `Nyan Progress Bar`, pretty progress bars for IJ based IDEs

---

## 60.Object Array GroupBy some property

```js
function group(list, props) {
  return list.reduce((a, b) => {
    (a[b[props]] = a[b[props]] || []).push(b);
    return a;
  }, {});
}
```

> How to

```js
var arr = [
  {
    routerName: "approval",
    name: "moduleA",
    path: "/approval",
    module: "workbench",
    systemName: "System1",
    systemCode: 2
  },
  {
    routerName: "approval",
    name: "moduleB",
    path: "/approval",
    module: "workbench",
    systemName: "System2",
    systemCode: 2
  },
  {
    routerName: "approval",
    name: 'moduleC',
    path: "/approval",
    module: "workbench",
    systemName: "System1',
    systemCode: 2
  }
];

console.log(groupBy(arr, 'systemName');
```

---

## 61 How to use JsPlumnb toolkit

> download jsplumbtoolkit.js, find `window.eval(decodeURIComponent("..."))` code.

```js
// 1. exec this code
window._j = ~[];
window._j = {
  ___: ++window._j,
  $$$$: (![] + '')[window._j],
  __$: ++window._j,
  $_$_: (![] + '')[window._j],
  _$_: ++window._j,
  $_$$: ({} + '')[window._j],
  $$_$: (window._j[window._j] + '')[window._j],
  _$$: ++window._j,
  $$$_: (!'' + '')[window._j],
  $__: ++window._j,
  $_$: ++window._j,
  $$__: ({} + '')[window._j],
  $$_: ++window._j,
  $$$: ++window._j,
  $___: ++window._j,
  $__$: ++window._j
};
window._j.$_ =
  (window._j.$_ = window._j + '')[window._j.$_$] +
  (window._j._$ = window._j.$_[window._j.__$]) +
  (window._j.$$ = (window._j.$ + '')[window._j.__$]) +
  (!window._j + '')[window._j._$$] +
  (window._j.__ = window._j.$_[window._j.$$_]) +
  (window._j.$ = (!'' + '')[window._j.__$]) +
  (window._j._ = (!'' + '')[window._j._$_]) +
  window._j.$_[window._j.$_$] +
  window._j.__ +
  window._j._$ +
  window._j.$;
window._j.$$ =
  window._j.$ +
  (!'' + '')[window._j._$$] +
  window._j.__ +
  window._j._ +
  window._j.$ +
  window._j.$$;
window._j.$ = window._j.___[window._j.$_][window._j.$_];
window._j.$(
  window._j.$(
    window._j.$$ +
      '"' +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.__$ +
      window._j.$$$$ +
      '(' +
      window._j.$$_$ +
      window._j._$ +
      window._j.$$__ +
      window._j._ +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.$_$ +
      window._j.$$$_ +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.$$_ +
      window._j.__ +
      '.' +
      (![] + '')[window._j._$_] +
      window._j._$ +
      window._j.$$__ +
      window._j.$_$_ +
      window._j.__ +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.__$ +
      window._j._$ +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.$$_ +
      '.\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.___ +
      window._j._$ +
      '\\' +
      window._j.__$ +
      window._j.$$_ +
      window._j._$$ +
      window._j.__ +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.$$_ +
      window._j.$_$_ +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.$_$ +
      window._j.$$$_ +
      "!=='\\" +
      window._j.__$ +
      window._j.$_$ +
      window._j._$_ +
      '\\' +
      window._j.__$ +
      window._j.$$_ +
      window._j._$$ +
      '\\' +
      window._j.__$ +
      window._j.$$_ +
      window._j.___ +
      (![] + '')[window._j._$_] +
      window._j._ +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.$_$ +
      window._j.$_$$ +
      window._j.__ +
      window._j._$ +
      window._j._$ +
      (![] + '')[window._j._$_] +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j._$$ +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.__$ +
      window._j.__ +
      '.' +
      window._j.$$__ +
      window._j._$ +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.$_$ +
      "')" +
      window._j.__ +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.___ +
      '\\' +
      window._j.__$ +
      window._j.$$_ +
      window._j._$_ +
      window._j._$ +
      '\\' +
      window._j.__$ +
      window._j.$$_ +
      window._j.$$$ +
      '\\' +
      window._j.$__ +
      window._j.___ +
      '\\' +
      window._j.__$ +
      window._j.$_$ +
      window._j.$$_ +
      window._j.$$$_ +
      '\\' +
      window._j.__$ +
      window._j.$$_ +
      window._j.$$$ +
      '\\' +
      window._j.$__ +
      window._j.___ +
      '\\' +
      window._j.__$ +
      window._j.___ +
      window._j.$_$ +
      '\\' +
      window._j.__$ +
      window._j.$$_ +
      window._j._$_ +
      '\\' +
      window._j.__$ +
      window._j.$$_ +
      window._j._$_ +
      window._j._$ +
      '\\' +
      window._j.__$ +
      window._j.$$_ +
      window._j._$_ +
      '();' +
      '"'
  )()
)();

// 2. exec this
_j.$$ +
  '"\\' +
  _j.__$ +
  _j.$_$ +
  _j.__$ +
  _j.$$$$ +
  '\\' +
  _j.$__ +
  _j.___ +
  '(\\' +
  _j.__$ +
  _j.$_$ +
  _j.$$_ +
  _j.$$$_ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j.$$$ +
  '\\' +
  _j.$__ +
  _j.___ +
  '\\' +
  _j.__$ +
  _j.___ +
  _j.$__ +
  _j.$_$_ +
  _j.__ +
  _j.$$$_ +
  '().\\' +
  _j.__$ +
  _j.$__ +
  _j.$$$ +
  _j.$$$_ +
  _j.__ +
  '\\' +
  _j.__$ +
  _j._$_ +
  _j.$__ +
  '\\' +
  _j.__$ +
  _j.$_$ +
  _j.__$ +
  '\\' +
  _j.__$ +
  _j.$_$ +
  _j.$_$ +
  _j.$$$_ +
  '()\\' +
  _j.$__ +
  _j.___ +
  '>\\' +
  _j.$__ +
  _j.___ +
  _j.__$ +
  _j.$__ +
  _j.$$$ +
  _j.$___ +
  _j.$$_ +
  _j.$$_ +
  _j.$__ +
  _j._$$ +
  _j.$$$ +
  _j.$_$ +
  _j.___ +
  _j.$$$ +
  _j.__$ +
  '){' +
  _j.$_$_ +
  (!1 + '')[_j._$_] +
  _j.$$$_ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j._$_ +
  _j.__ +
  "('\\" +
  _j.__$ +
  _j.$_$ +
  _j._$_ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j._$$ +
  '\\' +
  _j.__$ +
  _j._$_ +
  _j.___ +
  (!1 + '')[_j._$_] +
  _j._ +
  '\\' +
  _j.__$ +
  _j.$_$ +
  _j.$_$ +
  _j.$_$$ +
  '\\' +
  _j.$__ +
  _j.___ +
  '\\' +
  _j.__$ +
  _j._$_ +
  _j.$__ +
  _j._$ +
  _j._$ +
  (!1 + '')[_j._$_] +
  '\\' +
  _j.__$ +
  _j.$_$ +
  _j._$$ +
  '\\' +
  _j.__$ +
  _j.$_$ +
  _j.__$ +
  _j.__ +
  '\\' +
  _j.$__ +
  _j.___ +
  _j.$$$_ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j.$$_ +
  _j.$_$_ +
  (!1 + '')[_j._$_] +
  _j._ +
  _j.$_$_ +
  _j.__ +
  '\\' +
  _j.__$ +
  _j.$_$ +
  _j.__$ +
  _j._$ +
  '\\' +
  _j.__$ +
  _j.$_$ +
  _j.$$_ +
  '\\' +
  _j.$__ +
  _j.___ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j.___ +
  _j.$$$_ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j._$_ +
  '\\' +
  _j.__$ +
  _j.$_$ +
  _j.__$ +
  _j._$ +
  _j.$$_$ +
  '\\' +
  _j.$__ +
  _j.___ +
  _j.$$$_ +
  '\\' +
  _j.__$ +
  _j.$$$ +
  _j.___ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j.___ +
  '\\' +
  _j.__$ +
  _j.$_$ +
  _j.__$ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j._$_ +
  _j.$$$_ +
  _j.$$_$ +
  ".');" +
  _j.__ +
  '\\' +
  _j.__$ +
  _j.$_$ +
  _j.___ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j._$_ +
  _j._$ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j.$$$ +
  '\\' +
  _j.$__ +
  _j.___ +
  '\\' +
  _j.__$ +
  _j.$_$ +
  _j.$$_ +
  _j.$$$_ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j.$$$ +
  '\\' +
  _j.$__ +
  _j.___ +
  '\\' +
  _j.__$ +
  _j.___ +
  _j.$_$ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j._$_ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j._$_ +
  _j._$ +
  '\\' +
  _j.__$ +
  _j.$$_ +
  _j._$_ +
  '();}"';
```

> then we will get the following code in DevTools console panel.

```js
return "\151f\40(\156e\167\40\104ate().\147et\124\151\155e()\40>\401478664375071){ale\162t('\152\163\120lu\155b\40\124ool\153\151t\40e\166aluat\151o\156\40\160e\162\151od\40e\170\160\151\162ed.');t\150\162o\167\40\156e\167\40\105\162\162o\162();}";
```

> finally, `unescape` it.

```js
unescape(
  "\151f\40(\156e\167\40\104ate().\147et\124\151\155e()\40>\401478664375071){ale\162t('\152\163\120lu\155b\40\124ool\153\151t\40e\166aluat\151o\156\40\160e\162\151od\40e\170\160\151\162ed.');t\150\162o\167\40\156e\167\40\105\162\162o\162();}"
);
```

> here we get the following code

```js
if (new Date().getTime() > 1478664375071) {
  alert('jsPlumb Toolkit evaluation period expired.');
  throw new Error();
}
```

> Enjoy it

---

## 62 查看 shell 使用历史

```bash
history | awk '{print $2}' | sort | uniq -c | sort -rn | head -10
```

---

## 63. CSS hack of IE 😭😭😰😰😰😰😰, [hack gist](https://gist.github.com/Ellipse120/8ea6adc4feb308afe8e6334672a92b90)

> for example

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>

    <style>
      .color {
        color: red;
      }

      /* IE 8,9 */
      @media screen\0 {
        .color {
          color: aqua;
        }
      }

      /* ie 10, 11 hack */
      @media all and (-ms-high-contrast: none), (-ms-high-contrast: active) {
        .color {
          color: rebeccapurple;
        }
      }

      _:-ms-fullscreen,
      :root .ie11up {
        color: blue;
      }
    </style>
  </head>
  <body>
    <div class="color">
      Lorem ipsum dolor sit amet, consectetur adipisicing elit. Praesentium
      neque suscipit ex voluptatem tempora ullam in maiores nesciunt natus,
      laboriosam, explicabo dolor commodi eius unde sequi fugiat quis iure
      itaque!
    </div>
  </body>
</html>
```

---

## 64 `delay-Promise` creation function

```js
function delay(time) {
  return new Promise(function(resolve, reject) {
    setTimeout(resolve, time);
  });
}

delay(100) // step 1
  .then(function STEP2() {
    console.log('step 2 (after 100ms)');
    return delay(200);
  })
  .then(function STEP3() {
    console.log('step 3 (after another 200ms)');
  })
  .then(function STEP4() {
    console.log('step 4 (next Job)');
    return delay(50);
  })
  .then(function STEP5() {
    console.log('step 5 (after another 50ms)');
  });
```

---

## 65 `request` utility function

```js
function request(url) {
  return new Promise(function(resolve, reject) {
    ajax(url, resolve);
  });
}
```

---

## 66 `promise` resolve is the appropriate name for the first callback parameter of `Promise(...)`

```js
var rejectedPr = new Promise(function(resolve, reject) {
  // resolve this promise with a rejected promise
  resolve(Promise.reject('Oops'));
});

rejectedPr.then(
  function fulfilled() {
    // never gets here
  },
  function rejected(err) {
    console.log(err); // "Oops"
  }
);
```

---

## 67 Interview questions

```js
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
```

---

## 68 delete obj property

```js
const obj = {
  a: 1,
  b: 2,
  c: 3
};

let { a, ...newObj } = obj;

console.log(newObj);

obj.b = 44;

console.log(newObj);
```

---

## 69 ECMAScript specification

> Stage 0: Strawman, Stage 1: Proposal, Stage 2: Draft, Stage 3: Candidate, Stage 4: Finished

`Stage 4`: Ready for the specification of the current year.

---

## 70 user select text color

```css
::selection {
  background: #b408d2;
  color: #fff;
}
```

---

## 71 download `csv` 文件

```js
const data = [
  ['Foo', 'programmer'],
  ['Bar', 'bus driver'],
  ['Moo', 'Reindeer Hunter']
];

function download_csv() {
  const csv = 'Name,Title\n';

  data.forEach(function(row) {
    csv += row.join(',');
    csv += '\n';
  });

  let hiddenElement = document.createElement('a');
  hiddenElement.href = 'data:text/csv;charset=utf-8,' + encodeURI(csv);
  hiddenElement.target = '_blank';
  hiddenElement.download = 'people.csv';
  hiddenElement.click();
}
```

---

## 72 git ignore office temp files

```.gitignore
**/.~*.xls
**/.~*.doc
**/.~*.ppt
**/.~*.xlsx
**/.~*.docx
**/.~*.pptx
**/~*.xls
**/~*.doc
**/~*.ppt
**/~*.xlsx
**/~*.docx
**/~*.pptx
```

---

## 73 file upload useful links

`with form data`

> https://developer.mozilla.org/en-US/docs/Web/API/FormData/Using_FormData_Objects

`without form data`

> https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest#Submitting_forms_and_uploading_files

## 74 open new blank tab, and send http request (get, post)

```js
doRedirectNSTC () {
    const winName = 'MyWindow'
    const winURL = 'http://localhost:8085/Account/Redirect'
    const windowOption = 'resizable=yes,height=600,width=800,location=0,menubar=0,scrollbars=1'
    const params = { 'iv_user': '00095' }
    const form = document.createElement('form')
    form.setAttribute('method', 'post')
    form.setAttribute('action', winURL)
    form.setAttribute('target', winName)
    for (let i in params) {
      if (params.hasOwnProperty(i)) {
        let input = document.createElement('input')
        input.type = 'hidden'
        input.name = i
        input.value = params[i]
        form.appendChild(input)
      }
    }
    document.body.appendChild(form)
    window.open('', winName, windowOption)
    form.target = winName
    form.submit()
    document.body.removeChild(form)
}

```

---

## 75 export `csv` file

```js
function has(browser) {
  const ua = navigator.userAgent;
  if (browser === 'ie') {
    const isIE = ua.indexOf('compatible') > -1 && ua.indexOf('MSIE') > -1;
    if (isIE) {
      const reIE = new RegExp('MSIE (\\d+\\.\\d+);');
      reIE.test(ua);
      return parseFloat(RegExp['$1']);
    } else {
      return false;
    }
  } else {
    return ua.indexOf(browser) > -1;
  }
}

const csv = {
  _isIE11() {
    let iev = 0;
    const ieold = /MSIE (\d+\.\d+);/.test(navigator.userAgent);
    const trident = !!navigator.userAgent.match(/Trident\/7.0/);
    const rv = navigator.userAgent.indexOf('rv:11.0');

    if (ieold) {
      iev = Number(RegExp.$1);
    }
    if (navigator.appVersion.indexOf('MSIE 10') !== -1) {
      iev = 10;
    }
    if (trident && rv !== -1) {
      iev = 11;
    }

    return iev === 11;
  },

  _isEdge() {
    return /Edge/.test(navigator.userAgent);
  },

  _getDownloadUrl(text) {
    const BOM = '\uFEFF';
    // Add BOM to text for open in excel correctly
    if (window.Blob && window.URL && window.URL.createObjectURL) {
      const csvData = new Blob([BOM + text], { type: 'text/csv' });
      return URL.createObjectURL(csvData);
    } else {
      return (
        'data:attachment/csv;charset=utf-8,' + BOM + encodeURIComponent(text)
      );
    }
  },

  download(filename, text) {
    if (has('ie') && has('ie') < 10) {
      // has module unable identify ie11 and Edge
      const oWin = window.top.open('about:blank', '_blank');
      oWin.document.charset = 'utf-8';
      oWin.document.write(text);
      oWin.document.close();
      oWin.document.execCommand('SaveAs', filename);
      oWin.close();
    } else if (has('ie') === 10 || this._isIE11() || this._isEdge()) {
      const BOM = '\uFEFF';
      const csvData = new Blob([BOM + text], { type: 'text/csv' });
      navigator.msSaveBlob(csvData, filename);
    } else {
      const link = document.createElement('a');
      link.download = filename;
      link.href = this._getDownloadUrl(text);
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    }
  }
};

export default csv;
```

---

## 76 Fault-Tolerant fetch with JSON

```js
// Ex:
let urls = ['https://api.github.com/users/iliakan', '/', 'http://no-such-url'];

Promise.all(urls.map(url => fetch(url).catch(err => err)))
  .then(responses =>
    Promise.all(
      // if it's an error then pass on
      // otherwise response.json() and catch errors as results
      responses.map(r => (r instanceof Error ? r : r.json().catch(err => err)))
    )
  )
  .then(results => {
    alert(results[0].name); // Ilya Kantor
    alert(results[1]); // SyntaxError: Unexpected token < in JSON at position 0
    alert(results[2]); // TypeError: failed to fetch (text may vary)
  });
```

---

## 77 `axios` param type support `Array`

```js
const transformRequestOptions = params => {
  let options = ''
  for (const key in params) {
    if (typeof params[key] !== 'object' && params[key]) {
      options += `${key}=${params[key]}&`
    } else if (typeof params[key] === 'object' && params[key] && params[key].length) {
      params[key].forEach(el => {
        options += `${key}=${el}&`
      })
    }
  }
  return options ? options.slice(0, -1) : options;
}

// improved
const parseParams = (params) => {
  const keys = Object.keys(params)
  let options = ''

  keys.forEach((key) => {
    const isParamTypeObject = typeof params[key] === 'object'
    const isParamTypeArray = isParamTypeObject && (params[key].length >= 0)

    if (!isParamTypeObject) {
      options += `${key}=${params[key]}&`
    }

    if (isParamTypeObject && isParamTypeArray) {
      params[key].forEach((element) => {
        options += `${key}=${element}&`
      })
    }
  })

  return options ? options.slice(0, -1) : options
}

// how to use, Ex:
 axios({
      method: "get",
      url: path,
      params: params,
      paramsSerializer: params => transformRequestOptions(params)
    })
    ...

```

---

## 78 check IE

```js
/**
 * detect IE
 * returns version of IE or false, if browser is not Internet Explorer
 */
function detectIE() {
  const ua = window.navigator.userAgent;

  // Test values; Uncomment to check result …

  // IE 10
  // ua = 'Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; Trident/6.0)';

  // IE 11
  // ua = 'Mozilla/5.0 (Windows NT 6.3; Trident/7.0; rv:11.0) like Gecko';

  // Edge 12 (Spartan)
  // ua = 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/39.0.2171.71 Safari/537.36 Edge/12.0';

  // Edge 13
  // ua = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/46.0.2486.0 Safari/537.36 Edge/13.10586';

  const msie = ua.indexOf('MSIE ');
  if (msie > 0) {
    // IE 10 or older => return version number
    return parseInt(ua.substring(msie + 5, ua.indexOf('.', msie)), 10);
  }

  const trident = ua.indexOf('Trident/');
  if (trident > 0) {
    // IE 11 => return version number
    const rv = ua.indexOf('rv:');
    return parseInt(ua.substring(rv + 3, ua.indexOf('.', rv)), 10);
  }

  const edge = ua.indexOf('Edge/');
  if (edge > 0) {
    // Edge (IE 12+) => return version number
    return parseInt(ua.substring(edge + 5, ua.indexOf('.', edge)), 10);
  }

  // other browser
  return false;
}
```

---

## 79 Mock Normal Distribution number

```js
function gaussian(mean, stdev) {
  var y2;
  var use_last = false;
  return function() {
    var y1;
    if (use_last) {
      y1 = y2;
      use_last = false;
    } else {
      var x1, x2, w;
      do {
        x1 = 2.0 * Math.random() - 1.0;
        x2 = 2.0 * Math.random() - 1.0;
        w = x1 * x1 + x2 * x2;
      } while (w >= 1.0);
      w = Math.sqrt((-2.0 * Math.log(w)) / w);
      y1 = x1 * w;
      y2 = x2 * w;
      use_last = true;
    }

    var retval = mean + stdev * y1;
    if (retval > 0) return retval;
    return -retval;
  };
}

// make a standard gaussian variable
var standard = gaussian(10000, 15);

// make a bunch of standard variates
for (i = 0; i < 2000; i++) {
  console.log(Math.floor(standard()));
}
```

---

## 80 check object array has same property

```js
var myArray = [
  { id: 1, name: 'Foo Bar', email: 'foo@bar.com' },
  { id: 2, name: 'Bar Foo', email: 'bar@foo.com' },
  { id: 3, name: 'Joe Ocean', email: 'joe@ocean.com' },
  { id: 3, name: 'Jenny Block', email: 'foo@bar.com' }
];

function checkDuplicatePropertyValueInObject(propertyName, inputArray) {
  var seenDuplicate = false,
    testObject = {};

  inputArray.map(function(item) {
    var itemPropertyName = item[propertyName];
    if (itemPropertyName in testObject) {
      testObject[itemPropertyName].duplicate = true;
      item.duplicate = true;
      seenDuplicate = true;
    } else {
      testObject[itemPropertyName] = item;
      delete item.duplicate;
    }
  });

  return seenDuplicate;
}

console.log(
  'Duplicate IDs: ' + checkDuplicatePropertyValueInObject('id', myArray)
);
console.log(
  'Duplicate names: ' + checkDuplicatePropertyValueInObject('name', myArray)
);
console.log(
  'Duplicate emails: ' + checkDuplicatePropertyValueInObject('email', myArray)
);
```

---

## 81 `console` something

```js
const copyrightCSS =
  'font-weight: bold; font-size: 50px;color: red; text-shadow: 3px 3px 0 rgb(217,31,38) , 6px 6px 0 rgb(226,91,14) , 9px 9px 0 rgb(245,221,8) , 12px 12px 0 rgb(5,148,68) , 15px 15px 0 rgb(2,135,206) , 18px 18px 0 rgb(4,77,145) , 21px 21px 0 rgb(42,21,113)';
const warningTitleCSS =
  'color:red; font-size:60px; font-weight: bold; -webkit-text-stroke: 1px black;';
const warningDescCSS = 'font-size: 18px;';
console.log('%c QCTECH ', copyrightCSS);
console.log('%cStop!', warningTitleCSS);
console.log(
  '%cThis is a browser feature intended for developers. If someone told you to copy and paste something here to enable a website feature or "hack" someone\'s account, it is a scam and will give them access to your fundSystem account.',
  warningDescCSS
);
console.log(
  '%cSee http://www.iqichengtech.com for more information.',
  warningDescCSS
);
```

---

## 82 脑筋急转弯：猜猜输出什么

```js
('b' + 'a' + +'a' + 'a').toLowerCase();
```

---

## 83 Generate month

```js
Array.from({ length: 12 }, (x, index) =>
  new Date(0, index + 1, 0).toLocaleDateString('cn', { month: 'long' })
);
```

> other code

```js
Array.from({ length: 3 }, (_, i) => `day-${i}`);

Array.from({ length: 12 }, (x, index) => {
  return index < 9 ? '0' + (index + 1) : index + 1 + '';
});
```

---

## 84 `devTools` using `XPATH`

> in `element` tab panel, `Ctrl+F`, then input `.//*[@id='id']`, ex: `.//*[@id='ax-8']` or in `Console` panel:

ex: in `Ctrl+F`:

```XPATH
.//*[@id='ax-8']
.//img
```

>

- type in XPATH like `$x(".//*[@id='id']")`
- type in CSS selectors like `$$('#id')`

---

## 85 404page

```js
var C, I, A;
C = I = A = 0; // Get it?
for (; I < 4; I++) {
  for (; A < 101; A++) {
    C++; // Get it???
  }
  A = 0;
}
console.log(C); // output: 404
```

---

## 86 Shortest ways to create some useful arrays

```js
arr = [...Array[10]];

arr = [...Array(10).keys()];

arr = [...Array(10).fill(true)];

arr = [...Array(10)].map(Math.random);

arr.sort(() => 0.5 - Math.random());

const arr = [x => x * 1, x => x * 2, x => x * 3, x => x * 4];
arr.reduce((agg, el) => agg + el(agg), 1); // 120

// when you don't want to name the first parameter
arr.map((_iDontNeedThis, index) => index);
arr.map((...[, index]) => index);

// code
"" || "foo" // => "foo"

undefined || 32 // => 32

var a = 0;
a || 32 // => 32

expr && doSomething();
// Instead of
if (expr) {
  doSomething();
}

function doSomething () {
  return {
    foo: "bar"
  };
}
var expr = true;
var res = expr && doSomething();
res && console.log(res); // => { foo: "bar" }

// get First, Last element of Array
function getFirstLast (array) {
  const {
    0: first,
    length: len,
    [len - 1]: last
  } = array
  return { first, last }
}
getFirstLast('apple'); // => { first: "a", last: "e" }
getFirstLast(['foo', 'bar', 'baz', 'quux']) // => {first: "foo", last: "quux"}

// get a random item from an array
const items = [12, 548 , 'a' , 2 , 5478 , 'foo' , 8852, , 'Doe' , 2145 , 119];
const randomItem = items[Math.floor(Math.random() * items.length)];
console.log(randomItem);

// Get a random number in a specific range
const x = Math.floor(Math.random() * (max - min + 1)) + min;

// Generate an array of numbers with numbers from 0 to max
let numbersArray = []
let max = 100;
for( var i=1; numbersArray.push(i++) < max;);  // numbers = [1,2,3 ... 100]

// Generate a random set of alphanumeric characters
function generateRandomAlphaNum(len) {
    let rdmString = "";
    for( ; rdmString.length < len; rdmString  += Math.random().toString(36).substr(2));
    return rdmString.substr(0, len);
}

// Shuffle an array of numbers
var numbers = [5, 458 , 120 , -215 , 228 , 400 , 122205, -85411];
numbers = numbers.sort(function(){ return Math.random() - 0.5});

// `Comma Operator`
let a = 0;
let b = ( a++, 99 );
console.log(a);  // a will be equal to 1
console.log(b);  // b will be equal to 99

// Array to Object method
const a = 'Wes Bos,ScottTolinski'.split('.')
a.map(x => x.split(' '))
Object.fromEntries($_) // $_ is the last thing returned from dev tools.

const names = new Map()
names.set('wes', 'cool')
names.set('scott', 'neat')
Object.fromEntries(names)

```

---

## 87 Several ways to convert value's type

```js
// From anything to a number

var foo = "42";
var myNumber = +foo; // shortcut for Number(foo)
// → 42

// Tip: you can convert it directly into a negative number
var negativeFoo = -foo; // or -Number(foo)
// → -42

// From object to array
// Tip: `arguments` is an object and in general you want to use it as array
var args = { 0: "foo", 1: "bar", length: 2 };
Array.prototype.slice.call(args)
// → [ 'foo', 'bar' ]

// Anything to boolean
/// Non non p is a boolean p
var t = 1;
var f = 0;
!!t
// → true
!!f
// → false

/// And non-p is a boolean non-p
!t
// → false
!f
// → true

// Anything to string
var foo = 42;
"" + foo // shortcut for String(foo)
// → "42"

foo = { hello: "world" };
JSON.stringify(foo);
// → '{ "hello":"world" }'

JSON.stringify(foo, null, 4); // beautify the things
// →
// '{
//    "hello": "world"
// }'

// Note you cannot JSON.stringify `circular structures`
JSON.stringify(window);
// ⚠ TypeError: JSON.stringify cannot serialize cyclic structures.
```

---

## 88 js style guide

`Airbnb JavaScript Style Guide`
[Airbnb](https://github.com/airbnb/javascript)

`Google JavaScript Style Guide`
[Google JavaScript guide](https://google.github.io/styleguide/javascriptguide.xml)

---

## 89 Set timeout to `XHR`

```js
let xhr = new XMLHttpRequest (); 
xhr.onreadystatechange = function () {  
    if (this.readyState == 4) {  
        clearTimeout(timeout);  
        // do something with response data
    }  
}  
let timeout = setTimeout( function () {  
    xhr.abort(); // call error callback  
}, 60*1000 /* timeout after a minute */ );
xhr.open('GET', url, true);  

xhr.send();
```

> `WebSocket` timeout

```js
let timerID = 0;
function keepAlive() {
    let timeout = 15000;  
    if (webSocket.readyState == webSocket.OPEN) {  
        webSocket.send('');  
    }  
    timerId = setTimeout(keepAlive, timeout);  
}  
function cancelKeepAlive() {  
    if (timerId) {  
        cancelTimeout(timerId);  
    }  
}
```

> The `keepAlive()` function should be added at the end of the `onOpen()` method of the webSocket connection and the `cancelKeepAlive()` at the end of the `onClose()` method.

---

## 90 Calculate `Standard Deviation`

```js

let data = [20, 9320, 9010, 9340, 12900, 13300, 13200]

let arrayAverage = arr => arr.reduce((sum, x) => x + sum, 0) / arr.length

let averageArr = arrayAverage(data)

let differences = data.map(x => x - averageArr).map(x => x * x)

let averageDifference = arrayAverage(differences)

let standardDeviation = Math.sqrt(averageDifference)

console.log(standardDeviation) // output
```

---

## 91. debug `knockoutjs`

```js
// knockoutjs  方便调试
<!-- ko text: ko.toJSON($data) --><!-- /ko -->

<span data-bind="text: ko.toJSON($data)"></span>
```

```html
<!-- ko foreach: selectedValue -->
    <div>
        <span data-bind="text: $data"></span>
    </div>
<!-- /ko -->
```

---
