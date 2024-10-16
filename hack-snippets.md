# 记录开发中遇到的少见的，不常规的，解决后容易被忘记的问题

> 用`echarts`绘制的图在容器尺寸发生变化时重绘

- 如果容器的尺寸改变是由浏览器窗口改变引起的，监听`resize`事件就可以了。注意优化，使用`setTimeout`和`requestAnimation`等
- 如果浏览器窗口大小不变，其他因素引起的容器变化，如菜单折叠等

## 1.在引起容器尺寸变化的事件发生时强自触发`resize`事件，使用`jquery`的`resize`函数实现，实现代码如下

```js
$(window).resize()
```

---

## 2.监听相应的事件，在事件发生时调用`echarts`的`resize`函数，如折叠菜单发生时监听`transitionend`事件

```js
let eventTargert = document.getElementById('#nav')
eventTarget.addEventListener('transitionend', handleResize)
//cancle event listener
eventTarget.removeEventListener('transitionend', handleResize)
```

---

## 3
