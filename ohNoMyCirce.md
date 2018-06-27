ohNoMyCirce 经验分享
============================

项目[地址](https://github.com/djx314/ohNoMyCirce)和示例分享。

### 多余的复杂类型检查宏

#### 特点
1. 类型太过复杂，必须通过宏生成检查代码
1. 一般使用 implicitNotFound 作为编译错误提示信息展示手段（大部分情况下会结合伴生对象使用）
1. 绝大情况下避免直接使用宏报告错误，宏代码在任何时候都应该正常生成
1. 某些情况下可能会使用到非常复杂的 implicit 逻辑
1. 该部分代码几乎不会在运行时创建任何对象（部分情况下可能返回
Unit，但可通过其他方法使得实际上完全避免对象或引用的生成）
1. 基本不影响原有代码的逻辑，可以透明、随时地引入这些宏而无需担心会对现有代码或者性能造成影响
1. 依赖可有可无，删除检查代码后可以在发布前把相关依赖删除而不会造成任何影响

### 一些技巧
1. implicitNotFound 的类型信息插值  
经常会标记多余的无关的属性用来丰富提示信息  
属性名称这些类型无关信息可以在宏中拼接，这会导致每个属性要新建一个类型
implicitNotFound 的类型信息几乎是最完整的提示信息，个人觉得有可能优于宏
```scala
@implicitNotFound(msg = s"Can not find implicit value for Circe.\nCase Class Name: $${Model}\nProperty Type: $${Pro}\nProperty Name: testField\nImplicit Type: $${WrapPro}")
trait TestTrait[Model, Pro, WrapPro]
```
1. 属性不存在提示
```scala
@implicitNotFound(msg = s"$${Model} 类中，属性 id 不存在")
trait TestTrait[Model]
object TestTrait {
  implicit def modelImplicit1[M](implicit cv: M <:< { def id: Any }): TestTrait[M] = new TestTrait[M] { }
}
implicitly[TestTrait[MyCaseClassType]]
```
1. 更友好的类型信息
```scala
trait Implicit1[T1] {
  def require1(implicit cv: T1): T1 = cv
}
trait Implicit2[T2] {
  def require2(implicit cv: T2): T2 = cv
}
```

### 展望
1. 针对 shapeless 和 slick Table 的一些提示，做到报告出 HList 对应元素的索引号、类型、