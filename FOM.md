函数对象映射概念介绍
============================

项目[地址](https://github.com/scalax/asuna)和示例分享。

### 函数对象映射

asuna 是一个实现函数对象映射(Functional Object
Mapping)逻辑的库，或者更准确地说，是一个提供函数对象映射的容器。

最初设计灵感源自于 Slick 的 Shape，但没有采用 Slick 以 AST
作为数据容器的设计而直接使用了 List[Any]，这样能够更好地兼容各种不同数据类型的组合。

### 概念介绍

1. slick [代码](https://github.com/scalax/asuna/blob/master/src/test/scala/net/scalax/asuna/slick/simple/AsyncTest.scala#L32-L41)
重温
1. slick 的 Shape 的作用
1. 函数对象映射简介
[链接](https://github.com/scalax/asuna/blob/master/plan/%E9%A1%B9%E7%9B%AE%E5%88%9D%E6%9C%9F%E6%9E%84%E6%83%B3%EF%BC%88%E9%A1%B9%E7%9B%AE%E4%BB%A5%E8%8B%B1%E6%96%87%E4%B8%BA%E4%B8%BB%EF%BC%8C%E5%90%8E%E7%BB%AD%E5%88%A0%E9%99%A4%EF%BC%89.md#shape-%E4%BB%8B%E7%BB%8D)、
[TagAbs 源码 介绍](https://github.com/scalax/asuna/blob/master/core/src/main/scala/net/scalax/asuna/core/TagAbs.scala)
1. 第一个例子，链接同上（延迟计算逻辑，slick
的对接原理以及`<>`多次使用的坑的预防，[issue 地址](https://github.com/slick/slick/issues/1894)）
1. 针对 case class 的自动映射
[代码](https://github.com/scalax/asuna/blob/master/src/test/scala/net/scalax/asuna/slick/simple/AsyncTest.scala#L100-L115)
1. 丰富的错误提示（现场演示：属性不匹配，Shape 找不到，类型不匹配）
1. sangria 与 slick 整合
[示例代码（未美化）](https://github.com/scalax/asuna/blob/master/src/test/scala/net/scalax/asuna/aa/Def.scala)、
[实现代码（技巧部分）](https://github.com/scalax/asuna/blob/master/src/test/scala/net/scalax/asuna/aa/Def.scala)

完
============================