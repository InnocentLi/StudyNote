## 闭包    
### 闭包作用域
JS变量的作用域两种：全局变量和局部变量。
Javascript语言的特殊之处，就在于函数内部可以直接读取全局变量
```javascript
   var n=999;
　　function f1(){
　　　　alert(n);
　　}
　　f1(); // 999
  ```
函数外部自然无法读取函数内的局部变量。
  ```javascript
  　　function f1(){
　　　　var n=999;
　　}
　　alert(n) // error
  ```
函数内部声明变量的时候，不使用var命令会声明全局变量
  ```javascript
  function f1(){
　　　　n=999;
　　}
　　f1();
　　alert(n);
  ```
从外部读取局部变量
  ```javascript
  　　function f1(){
　　　　var n=999;
　　　　function f2(){
　　　　　　alert(n); // 999
　　　　}
　　}
```
但是f2内部的局部变量，对f1就是不可见的
这就是Javascript语言特有的"链式作用域"结构（chain scope），子对象会一级一级地向上寻找所有父对象的变量。所以，父对象的所有变量，对子对象都是可见的，反之则不成立。
既然f2可以读取f1中的局部变量，那么只要把f2作为返回值，我们就可以在f1外部读取它的内部变量了！
```javascript
function f1(){
　　　　var n=999;
　　　　function f2(){
　　　　　　alert(n); 
　　　　}
　　　　return f2;
　　}
　　var result=f1();
　　result(); // 999
```
### 闭包的用途    
闭包可以用在许多地方。它的最大用处有两个，一个是前面提到的可以读取函数内部的变量，另一个就是让这些变量的值始终保持在内存中。
```javascript
function f1(){
　　　　var n=999;
　　　　nAdd=function(){n+=1}
　　　　function f2(){
　　　　　　alert(n);
　　　　}
　　　　return f2;
　　}
　　var result=f1();
　　result(); // 999
　　nAdd();
　　result(); // 1000
  ```
  

