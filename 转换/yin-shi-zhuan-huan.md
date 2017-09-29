# 隐式转换

存在以下隐式转换：

* 标识转换
* 隐式数值转换
* 隐式枚举转换
* 可以为null的隐式转换
* null文本转换
* 隐式引用转换
* 装箱转换
* 隐式动态转换
* 隐式常量表达式转换
* 用户自定义的隐式转换
* 匿名函数转换
* 方法组转换

隐式转换可以发生在多种情况下：

* 函数成员调用；
* 强制转换表达式；
* 赋值；

## 标识转换

？

## 隐式数值转换

* 从sbyte到short、int、long、float、double、decimal；
* 从byte到short、ushort、int、uint、long、ulong、float、double、decimal；
* 从short到int、long、float、double、decimal；
* 从ushort到int、uint、long、ulong、float、double、decimal；
* 从int到long、float、double、decimal；
* 从uint到long、ulong、float、double、decimal；
* 从long或ulong到float、double、decimal；
* 从chat到ushort、int、uint、long、ulong、float、double、decimal；
* 从float都double；

## 隐式枚举转换

？

## 可以为null的隐式转换

？

## null文本转换

* 从null文本到任何可以为null的任何类型；

## 隐式引用转换

引用转换会更改引用的类型，但绝不会更改引用对象的类型或值；

* 从任何引用类型到object和dynamic；
* 从任何派生类类型到任何基类类型和基接口类型；
* 从任何派生接口类型到任何基接口类型；
* 从元素类型为S的数组到元素类型为T的数组（前提：两个数组只有元素不同；S和T都是引用类型；存在从S到T的隐式转换）；
* 从任何数组类型到System.Array类型和基接口类型；
* 从一维数组S\[\]到System.Collections.Generic.IList&lt;T&gt;及其基接口类型；
* 从任何委托类型到System.Delegate类型及其基接口类型；

## 装箱转换

* 从任何不可空值类型到object、dynamic、System.ValueType以及基接口类型的装箱转换；
* 枚举类型到System.Enum类型；

## 隐式动态转换

* 从dynamic类型的表达式到任何类型的隐式动态转换（可能引发运行时异常）；
  ```
  dynamic d = "dynamic";
  string s = d;    //存在隐式动态转换
  int i = d;        //引发异常
  ```

## 隐式常量表达式转换

* 从int类型的常量到sbyte、byte、short、ushort、uint和ulong类型的常量；
* 从long类型的常量到ulong类型的常量；

## 涉及类型形参的隐式转换

对于给定的类型形参T：

* 从T到任何有效基类C、从T到C的任何基类、从T到C的任何基接口；
* 从T到有效接口集中的接口类型I、从T大I的任何基接口；
* 从T到类型形参U（前提：T依赖U）；
* 从null文本到T；

？

## 用户定义的隐式转换

？

## 匿名函数转换和方法组转换

匿名函数和方法组本身没有类型。

* 从匿名函数或方法组到委托类型或表达式树类型；



