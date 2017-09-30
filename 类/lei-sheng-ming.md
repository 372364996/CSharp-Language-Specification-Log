# 类声明

\[attributes\] \[class-modifiers\] \[partial\] class identifier \[&lt;type-parameter-list&gt;\] \[:class-base\] \[type-parameter-constraints-clauses\] class-body \[;\]

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

用于防止从所修饰的类派生出其它类型。密封类不能同时是抽象类。

密封类可促使某些运行时优化，具体而言，因为密封类不能有任何派生类，因此对密封类的实例的**虚函数成员**的调用可以转换为非虚调用来处理。

static修饰符（静态类）：

用于标记声明为静态类。静态类不能实例化，仅可以包含静态成员。**只有静态类可以包含扩展方法的声明**。

静态类声明受到以下限制：

1. 静态类不能包含sealed、abstract修饰符，但静态类的行为既好像是密封的（不能派生），又好像是抽象的（不能实例化）。
2. 静态类不能显示指定基类或接口，静态类默认从object派生；
3. 静态类只能包含静态成员（**常量和嵌套类型属于静态成员**）；
4. 静态类不能含有可访问性为protected或protected internal的成员。
5. 静态类不能有任何实例构造函数，编译器对静态类不提供默认实例构造函数。
6. 静态类不可用于数组类型、指针类型、new表达式、强制类型转换、is表达式、as表达式、sizeof表达式或default表达式。

## partial（部分）修饰符

用于声明分部类型。

## 类型形参

代表一个占位符，在创建类型实例时指定类型实参来填充。该特性应用在泛型类型声明中。

## 类基本规范

用于定义该类的直接基类和实现的接口。

基类：

* 如果泛型类声明中制定了基类，则基类的每个类型形参替换为构造类型对应了类型形参：
  ```
  class B<U,V> {...}
  class G<T>: B<string,T[]> {...}
  ```
* 类类型的直接基类必须至少与类类型本身具有相同的可访问性：
  ```
  internal class A {...}
  public class B: A {...}    //编译时错误
  internal class C: A {...}    //正确
  ```
* 类类型的直接基类不能为下列类型：System.Array、System.Delegate、System.MulticastDelegate、System.Enum、System.ValueType。
* 泛型类声明不能将System.Attribute用作直接或间接基类。
* 一个类类型的基类包含直接基类以及直接基类的基类，基类集是直接基类关系的传递闭包。
  ```
  class A {...}
  class B: A {...}    //B的基类集包含A和object
  ```
* 类依赖于它的直接基类（传递闭包），还依赖于它的外围类（自反：所嵌套在其中的类），即：一个类所依赖的类的完备集就是此依赖关系的自反和传递闭包。
  ```
  class A: A {...}    //错误：类不能依赖于自身

  class X: Y {...}
  class Y: Z {...}
  class Z: X {...}    //错误：类之间循环依赖

  class M: N.E {...}
  class N: M
  {
      public class E {...}
  }                    //错误：M依赖于N.E，N.E依赖于N，N依赖于M，循环依赖了

  ```
* 类不依赖于内部的嵌套类；
  ```
  class A
  {
      class B: A {...}    //类B依赖于A，类A不依赖于B
  }
  ```

## 类型形参约束

where T : 约束列表（一个主约束、一个或多个次要约束、构造函数约束new\(\)）

每个类型形参只能有一个where子句。

主约束：可以是类类型、引用类型约束**class**，也可以是值类型约束**struct**。

次要约束：**类型约束**或**接口约束**。

class约束：指定类型实参必须是引用类型。

* 不能是sealed密封类；

* 不能是以下类型之一：System.Array、System.Delegate、System.Enum、System.ValueType。
* 不能是object；
* 只能有一个类类型约束

struct约束：指定类型实参必须是不可为null的值类型。

类型约束：

* where子句中每个类型只能指定一次。

接口约束：

* where子句中每个接口只能指定一次。

## 类体

用于定义类的成员。

