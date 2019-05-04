---
title: A 10-Minute Introduction to Scala
author: 李新星
date: 20190505
theme: gaia
---
>注: 该分享的正文内容来自于一遍英文介绍, 有 js 和 python 基础的可以直接阅读[原文链接](https://hackernoon.com/a-10-minute-introduction-to-scala-d1fed19eb74c)

# A 10-Minute Introduction to `Scala` 

![](https://cdn-images-1.medium.com/max/800/1*QFgSZTYpRbyxfti-ouAbtA.png)

---
# Why Scala ?
北京中科院计算所, 标签化团队使用 Scala 语言
![](https://i.loli.net/2019/05/04/5ccd8af972d4c.png)

---
- Scala is a programming language released in 2004 by Martin Odersky.

- It provides support for **functional programming** and is designed to be concise and compiled to **Java bytecode** so that a Scala application can be executed on a Java Virtual Machine (JVM).
---
# If let you design a new language, what is necessary ?

- `Variables` , Type, isImmutable?
- `If` , `for`
- `Function`, method or function
- `Object` or `Class`
    - Singleton
    - extends
    - List : [0,1,2,3] , Map : { "age" : "1" }
---

# Const Values 
```
val v1: String = "foo"
val v2 = "bar"
```
The type is optional. v1 and v2 are both typed as a String.

The Scala compiler can infer the type of a value without having to explicitly declare it. This is known as **type inference**.

A value in Scala is immutable. 
```
val i = 0
i = 1 // Compilation error
```
---
# Variables
A variable is a mutable value. It is declared with the var keyword.
```scala
var counter = 0
counter = counter + 5
```
Furthermore, Scala is a **statically typed language**. The following code, for example, is invalid as we try to map an Int into a variable already defined as a String:
```
var color = "red"
color = 5 // Invalid
```
---
# Blocks
```
println(7) // Prints 7

println {
  val i = 5
  i + 2
} // Prints 7
```
---
# String Interpolation
```js
"Hello $name"   // php
`Hello ${name}` // js
```
scala
```scala
val name = "Bob"
println(s"Hello $name!") // Hello Bob!
```
---
# Array and List
```scala
val a = new Array[Int](2)
val b = Array(0,1)
a(0) = 0
b(1) = 2
```
Compared to Array, modifying an index after having initialized a List will lead to a compilation error.
```scala
val list = List(5, 2)
list(0) = 5 // Compilation error
```
---
# Map
Note the `->` operator to associate a color key to its corresponding hexadecimal value.
```scala
val colors1 = Map("red" -> "#FF0000", "azure" -> "#F0FFFF", "peru" -> "#CD853F")
val colors2 = colors1 + ("blue" -> "#0033FF")
```
Map is an immutable data structure. Adding an element means creating another Map.

---
# Function
```scala
def add(x: Int, y: Int): Int = {
  x + y
}
```
The `return` keyword is optional.

---
# Function
```scala
def add(x: Int = 1, y: Int): Int = {
  x + y
}
add(_,2) //3
```
we can define default parameters value like above,

---
# Function

or use list args.
```scala
def variablesArguments(args: Int*): Int = {
  var n = 0
  for (arg <- args) {
    n += arg
  }
  n
}
```
---
# If-else
If-else syntax is similar in Scala than in several other languages:
```scala
if (condition1) {

} else if (condition2) {

} else {

}
```
Yet, in Scala an if-else statement is also an expression
```scala
def max(x: Int, y: Int) = if (x > y) x else y
```
---
# Loops
```scala
// Include
for (a <- 0 to 10) {
 println(a)
}
// Exclude
for (a <- 0 until 10) {
 println(a)
}

// We can also loop over two elements:
for (a <- 0 until 2; b <- 0 to 2) {
  
}
```
---
# Nested Functions
Let’s consider the following example:
```scala
def mergesort1(array: Array[Int]): Unit = {
  val helper = new Array[Int](array.length)
  mergesort2(array, helper, 0, array.length - 1)
}

private def mergesort2(array: Array[Int], helper: Array[Int], low: Int, high: Int): Unit = {
  if (low < high) {
    val middle = (low + high) / 2
    mergesort2(array, helper, low, middle)
    mergesort2(array, helper, middle + 1, high)
    merge(array, helper, low, middle, high)
  }
}
```
---
# Nested Functions
Yet, in Scala we can also decide to nest the second method into the first one like that:
```scala
def mergesort1(array: Array[Int]): Unit = {
  val helper = new Array[Int](array.length)
  mergesort2(array, helper, 0, array.length - 1)

  def mergesort2(array: Array[Int], helper: Array[Int], low: Int, high: Int): Unit = {
    if (low < high) {
      val middle = (low + high) / 2
      mergesort2(array, helper, low, middle)
      mergesort2(array, helper, middle + 1, high)
      merge(array, helper, low, middle, high)
    }
  }
}
```
---
# Function Literals
Scala is considered as a functional language in the sense that every function is a value.
```scala
val increment: Int => Int = (x: Int) => x + 1

println(increment(5)) // Prints 6
```
```scala
def foo(i: Int, f: Int => Int): Int = {
  f(i)
}
```
---
# Currying
```scala 
def multiply(n1: Int)(n2: Int): Int = {}
def multiply2(n1: Int, n2: Int): Int = {
  n1 * n2
}
```

Yet, the way to call multiply is different:
```scala
val n = multiply(2)(3)
```
we can partially applied multiply which gives us an Int => Int function.
```scala
val partial: Int => Int = multiply(2)
```

---
# 总结
- 脚本语言的语法糖, 可被 c++ 简单实现
    - 不同的 `If-else` `Loop`语法
    - `val`不变量, 自动推断类型的`var`变量
    - 普通函数定义, 动态参数,默认值
- 脚本语言的`特殊点` , 非语法糖部分
    - 函数闭包
    - Curry 化
    - 箭头函数 `val increment: Int => Int = (x: Int) => x + 1`, 换个说法, "lamda 表达式"

---
# 延伸阅读
- [A 10-Minute Introduction to Scala](https://hackernoon.com/a-10-minute-introduction-to-scala-d1fed19eb74c)
- [Scala 函数式编程](https://zhuanlan.zhihu.com/p/25484213)
- [Scala - 菜鸟教程](https://www.runoob.com/scala/scala-tutorial.html)
