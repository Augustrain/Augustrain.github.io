---
layout: post
title:  "Python学习手册 笔记（第六章）"
categories: Python
tags: Python学习手册
excerpt: python的核心是动态。
---

## 第6章 动态类型简介
### 缺少类型声明语句的情况
* python中，类是在运行中自动决定的

### 变量、对象和引用
* python赋值时的操作：1.创建一个对象来代表3；2.创建一个变量a，如果他还没有被创建；3.将变量与新的对象3相连接。
* 变量和对象保存在内存中的不同部分，通过连接相关联。变量总是连接到对象，绝不会连接到其他变量上，但是更大的对象可能连接到其他的对象（如列表等）
* 从变量到对象的连接称作引用
* 变量被使用，python自动跟随这个变量到对象的连接
* 1.变量时一个系统表的元素，拥有指向对象的连接的空间；2.对象是分配的一块内存，有足够的空间去表示它们所代表的值；3.引用是自动形成从变量到对象的指针
* 每一个对象都有两个标准的头部信息：一个类型标志符去标识这个对象的类型，一个引用的计数器，决定是不是可以回收这个对象

### 类型属于对象，而不是变量
* python的引用类似于c的指针。事实上，引用是以指针的形式实现的。
* 修改变量，只是修改了对不同对象的引用
* 对象知道自己的类型。每个对象包含一个头部信息，包含了每个对象的类型。例如，整数对象3，包含了值3和一个头部信息，这是一个整数对象（严格上，一个指向int的对象的指针）；'spam'字符串的对象的标志符指向一个字符串类型

### 对象的垃圾收集
* 每个变量名被赋予一个新的对象，之前对象占用的空间会被收回（如果他没有被其他的变量名或对象所引用）。这种自动回收对象空间的技术叫做垃圾收集。
* 每个对象中保持了一个计数器，计数器记录了当前指向该对象的引用的数目。一旦计数器为0，这个对象的内存空间会被自动回收。
* 意味着在脚本中任意使用对象不需要考虑释放内存空间
* python循环检查器的更多细节，参见python库手册中gc模块文档

### 共享引用
* a和b引用了相同的对象，称为共享引用

### 共享引用和在原处修改
```python3
L1 = [2, 3, 4]
L2 = L1
```
* 列表中的元素是通过位置进行读取的，L1[0]引用了对象2
* 列表自身也是对象
```python3
L1 = [2, 3, 4]
L2 = L1
L1[0] = 24
L1 # [24, 3, 4]
L2 # [24, 3, 4]
```
* 没有改变L1，改变了L1所引用对象的一个元素
* 如果你不想这样的现象发生，需要python拷贝对象，而不是创建引用。复制一个字典或集合应用X.copy()

### 共享引用和相等
* ==操作符，测试两个被引用对象是否有相同的值；is操作符，检查对象的同一性，实际上，is只是比较实现引用的指针
```python3
X = 42
Y = 42
X == Y # True
X is Y # True
```
* 原因是小的整数和字符串被缓存并复用了,是为了执行速度而采用的优化其模块的众多方法之一
* sys模块中的getrefcount函数会返回对象的引用次数

### 动态类型随处可见
* 动态类型是python中多态的根本