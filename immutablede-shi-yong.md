# immutable

##介绍说明

- 简介
 > Immutable Data 就是一旦创建，就不能再被更改的数据。对 Immutable 对象的任何修改或添加删除操作都会返回一个新的 Immutable 对象。
 
- 原理
 >Immutable 实现的原理是 Persistent Data Structure（持久化数据结构），也就是使用旧数据创建新数据时，要保证旧数据同时可用且不变。同时为了避免 deepCopy 把所有节点都复制一遍带来的性能损耗，Immutable 使用了 Structural Sharing（结构共享），即如果对象树中一个节点发生变化，只修改这个节点和受它影响的父节点，其它节点则进行共享。
 
- 使用原因
 >JavaScript 中的对象一般是可变的（Mutable），因为使用了引用赋值，新的对象简单的引用了原始对象，改变新的对象将影响到原始对象。
 如 foo={a: 1}; bar=foo; bar.a=2 你会发现此时 foo.a 也被改成了 2。虽然这样做可以节约内存，但当应用复杂后，这就造成了非常大的隐患，Mutable 带来的优点变得得不偿失。为了解决这个问题，一般的做法是使用 shallowCopy（浅拷贝）或 deepCopy（深拷贝）来避免被修改，但这样做造成了 CPU 和内存的浪费
 
- 优点
 >  - 降低了 Mutable 带来的复杂度。可变（Mutable）数据耦合了 Time 和 Value 的概念，造成了数据很难被回溯，但是immutable Data 没有这个问题。
  - 节省内存，Immutable 使用了 Structure Sharing 会尽量复用内存，甚至以前使用的对象也可以再次被复用。没有被引用的对象会被垃圾回收。
  - Undo/Redo，Copy/Paste，甚至时间旅行这些功能做起来小菜一碟
  - 并发安全,传统的并发非常难做，因为要处理各种数据不一致问题，因此『聪明人』发明了各种锁来解决。但使用了 Immutable 之后，数据天生是不可变的，并发锁就不需要了。

## 导航

  1. [常用方法介绍](immutablede-shi-yong/chang-yong-fang-fa-jie-7ecd-md.md)
  1. [项目中的使用](immutablede-shi-yong/xiang-mu-zhong-de-shi-7528-md.md)








