# 值类型的默认值

* 所有简单类型：默认值是由所有位都置零的位模式产生的：

* * sbyte、byte、short、ushort、int、uint、long和ulong默认值为0；
  * char默认值为'\x0000';
  * float默认值为0.0f;
  * double默认值为0.0d;
  * decimal默认值为0.0m;
  * bool默认值为false;
* 枚举类型：默认值是0，该值被转换为枚举类型。
* 结构类型：默认值是将所有值类型的字段设为它们的默认值并将所有引用类型设为null而产生的值。



