# 显示转换

存在一下显示转换：

* 所有隐式转换；
* 显示数值转换；
* 显示枚举转换；
* 可以为null的显示转换；
* 显示引用转换；
* 显示接口转换；
* 拆箱转换；
* 显示动态转换；
* 用户定义的显示转换；

显示转换发生在一下情况：

* 强制转换表达式中；

## 所有隐式转换

* 使用冗余的强制转换表达式；

## 显示数值转换

显示数值转换可能丢失数据精度或引发异常。

* 从 sbyte 到 byte、ushort、uint、ulong 或 char。
* 从 byte 到 sbyte 和 char。
* 从 short 到 sbyte、byte、ushort、uint、ulong 或 char。
* 从 ushort 到 sbyte、byte、short 或 char。
* 从 int 到 sbyte、byte、short、ushort、uint、ulong 或 char。
* 从 uint 到 sbyte、byte、short、ushort、int 或 char。
* 从 long 到 sbyte、byte、short、ushort、int、uint、ulong 或 char。
* 从 ulong 到 sbyte、byte、short、ushort、int、uint、long 或 char。
* 从 char 到 sbyte、byte 或 short。
* 从 float 到 sbyte、byte、short、ushort、int、uint、long、ulong、char 或 decimal。
* 从 double 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float 或 decimal。
* 从 decimal 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float 或 double。

引发异常的情况：

* 在checked上下文中（默认），如果源操作数不在目标操作数的范围内，会引发System.OverflowException异常。
* 从decimal到整型的转换，会向零舍入得到最近的整数值，如果得到的整数值在目标范围之外，会引发System.OverflowException异常。
* 从float或double到整型的转换，在checked上下文中，如果**源操作数是NaN或无穷大**，将引发System.OverflowException异常；否则源操作数向零舍入得到最近的整数值，如果该值超出目标范围，则引发System.OverflowException异常。

## 显示枚举转换

* 从 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 decimal 到任何 enum-type。
* 从任何 enum-type 到 sbyte、byte、short、ushort、int、uint、long、ulong、char、float、double 或 decimal。
* 从任何 enum-type 到任何其他 enum-type。

两种枚举类型之间的显示转换是将枚举转换为基础类型后，在产生的基础类型之间执行隐式或显示数值转换进行的。

## 可以为null的显示转换

如果不可以为null的值类型S到不可以为null的值类型T可以转换，那么也存在：

* 从S?到T?的显示转换；
* 从S到T?的显示转换；
* 从S?到T的显示转换；

## 显示引用转换

* 从object和dynamic到任何其他引用类型；
* 从任何基类类型到任何派生类类型；
* 从任何类类型到任何接口类型（前提：类类型不是密封的，且未实现该接口）；
* 从任何接口类型到任何类类型（前提：类类型不是密封的或实现了该接口）；
* 从任何接口类型到任何接口类型（前提：不是派生关系）；
* 从元素类型为S的数组到元素类型为T的数组（前提：数组具有相同的维度；元素类型都是引用类型；存在从S到T的显示引用转换；
* 从System.Array及其实现的接口到任何数组类型；
* 从一维数组S\[\]到System.Collections.Generic.IList&lt;T&gt;及其基接口（前提：存在从S到T的显示引用转换）；
* 从System.Delegate及其实现的接口到任何委托类型；

## 拆箱转换

* 从引用类型到值类型；

## 显示动态转换

* 从dynamic到任何类型；该过程如果失败则引发异常；
  ```
  class C
  {
  	int i;
  	public C(int i) { this.i = i; }
  	public static explicit operator C(string s) 
  	{
  		return new C(int.Parse(s));
  	}
  }
  下面的示例说明显式动态转换：
  object o  = "1";
  dynamic d = "2";
  var c1 = (C)o; // 显示引用转换，该过程会失败，因为"1"实际上不是C类型
  var c2 = (C)d; // 显示动态转换，该过程会成功
  ```



