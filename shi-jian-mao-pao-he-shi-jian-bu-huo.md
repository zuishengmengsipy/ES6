# 事件冒泡和事件捕获

事件传递有两种方式：冒泡与捕获。事件传递定义了元素事件触发的顺序。

在 冒泡 中，内部元素的事件会先被触发，然后再触发外部元素，即：  元素的点击事件先触发，然后会触发  元素的点击事件。

在 捕获 中，外部元素的事件会先被触发，然后才会触发内部元素的事件 

![](.gitbook/assets/image%20%284%29.png)

**事件冒泡**

```javascript
<script>
  var box = document.querySelector('.box');
  var content = document.querySelector('.content');
  document.addEventListener('click', function(e) {
    console.log('document');
  }, false);
  document.body.addEventListener('click', function(e) {
    console.log('body');
  }, false);
  box.addEventListener('click', function(e) {
    console.log('box');
  }, false);
  content.addEventListener('click', function(e) {
    console.log('content');
  }, false);
</script>
```

当我们点击.content时，事件的执行顺序是content - box - body - document。所以事件冒泡的走向是由子节点向父节点去触发同名事件

**事件捕获**

```javascript
<script>
  var box = document.querySelector('.box');
  var content = document.querySelector('.content');
  document.addEventListener('click', function(e) {
    console.log('document');
  }, true);
  document.body.addEventListener('click', function(e) {
    console.log('body');
  }, true);
  box.addEventListener('click', function(e) {
    console.log('box');
  }, true);
  content.addEventListener('click', function(e) {
    console.log('content');
  }, true);
</script>
```

当我们点击.content时，事件的执行顺序是document - body - box - content。所以事件捕获的走向是由父节点向子节点去触发同名事件

**总结：**

```text
addEventListener('', function(e) {}, false);
```

第三个参数可控制事件是冒泡还是捕获，js逻辑写法的先后顺序与事件触发的顺序无关

作者：[KeerDi](http://www.cnblogs.com/keerdi/) —— **ET.frog**  
  
出处：[http://www.cnblogs.](http://www.cnblogs.com/frogblog/)

