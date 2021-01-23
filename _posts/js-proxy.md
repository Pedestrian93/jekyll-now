# Proxy 与 Reflection

### 前言

ES6 中数组存在的缺陷：

当改变数组元素时，数组的长度会受影响，反过来也一样。



### 介绍 Proxy

使用 `new Proxy()` 会创建一个 proxy 对象，该对象会虚拟化目标对象，所以实际上可以认为它们是同一个对象。

```javascript
const proxy = new Proxy(target, handler);
```

`handler` 为一个有一批特殊属性的占位符对象，包含若干 `Proxy`的捕获器。

 



````javascript
const a = 1;
````

