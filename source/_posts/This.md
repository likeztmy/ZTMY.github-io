---
title: this
---
this: 在面向对象语言中，this用于指向当前对象，其类型为object，其值为当前对象
---
## this在方法中的使用 ##
```
var person = {
  name : '张三'，
  fullName : function() {
    return this.name;
  }
}; 
person.fullName(); //张三
```

## this在函数中的使用 ##

### 1.在标准函数中的使用 ###
this 指向的是把函数当成方法调用的上下文对象

```
var color= 'red';
var o = {
    color: 'blue'
};

function sayColor() {
    console.log(this.color)
};

sayColor(); //red

o.fn = saycolor;
o.fn(); //blue
```

### 2.在箭头函数中的使用 ###
this 指向的是定义箭头函数的上下文
```
var color = 'red';
var o = {
    color : 'blue'
};

var sayColor = () => console.log(this.color);

sayColor(); //red

o.fn = sayColor;
o.fn(); //red
```

### 3.闭包 ###
```
obj = {
    fn: function () {
            return function () {
                console.log(this);
        }
    }
};

obj.fn()();
```

## this在事件中使用 ##
```
<input type="button" value="按钮" onclick="console.log(this)">
```

## this单独使用 ##
```
var x = this;
console.log(x); // window
```

## call() 和 apply() ##

### 1. call()方法 ###
```
//语法规则：
//函数名称.call(obj,arg1,arg2,arg3....);
//obj：函数内this要指向的对象
//arg1,arg2,arg3...:要传递的参数

var obj = {name: '张三'}；

function fn(age) {
    console.log(this.name);
    console.log(age);
}

fn.call(obj,18); //张三 18
```

### 2. apply()方法 ###
```
//语法规则：
//函数名称.apply(obj,[arg1,arg2,arg3...])
//obj: 函数内this要指向的对象
//[agr1,arg2,arg3...]:要传递的参数，要求格式为数组

var obj = {name: '张三'}；

function fn(age,sex) {
    console.log(this.name);
    console.log(age);
	console.log(sex);
}

fn.apply(obj,[18,'man']); //张三 18 man
```

### 3. bind()方法 ###
```
// 跟 apply()方法，call()方法 有所区别
// bind()方法会创建一个新的函数实列
// 语法规则：
// 函数名称.bind(obj,arg1,arg2,arg3)
// obj: 新的函数中this要绑定的对象
// arg1,arg2,arg3...:要传递的参数

var color = 'red';
var o = {
    color = 'blue'
};

function sayColor() {
    console.log(this.color);
}

let fn = sayColor.bind(o);
fn(); //blue
```

## 测试 ##

```
var o = {
    f1: function f1(){
            function f2(){
                console.log(this);
            }
            f2();
    },
    f3: function f3() {
            let f4 = () => {
                console.log(this);
            }
            f4();
        }
}
obj.f1();
obj.f3();
```
