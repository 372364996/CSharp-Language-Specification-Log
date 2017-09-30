# 类声明

\[attributes\] \[class-modifiers\] \[partial\] class identifier \[type-parameter-list\] \[class-base\] \[type-parameter-constraints-clauses\] class-body \[;\]

* attributes:特性
* class-modifiers:类修饰符

* partial:部分类

* type-parameter-list:类型形参，泛型类声明使用

* class-base:类基本规范

* type-parameter-constraints-clauses:类型形参约束

* class-body:类体

## 类修饰符

* new
* public
* protected
* internal
* private
* abstract
* sealed
* static

new修饰符：

用于隐藏同名的继承成员。

public、protected、internal、private修饰符：

用于控制类的可访问性。

abstract修饰符（抽象类）：

用于表示所修饰的类是**不完整**的，并且只能用作基类。

抽象类于非抽象类的区别：

1. 抽象类不能实例化；
2. 抽象类可以包含抽象成员；
3. 抽象类不能被密封（因为必须要有派生类）；

当从抽象类派生非抽象类时，非抽象类必须实现所有抽象成员。

sealed修饰符（密封类）：







