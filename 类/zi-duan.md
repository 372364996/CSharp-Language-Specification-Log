# 字段

字段是一种表示与对象或类关联的**变量**的成员。

## 静态字段和实例字段

当字段的声明中使用**static**修饰符时，该字段为静态字段。不使用static修饰符声明的字段称为实例字段。

静态字段在对象的所有实例之间共享，静态字段在应用程序域中只有一个副本。

## 只读字段

当字段的声明中使用**readonly**修饰符时，该字段为只读字段。

只读字段只能在以下情况下赋值：

1. 只读字段声明时；
2. 类型的静态构造函数中；
3. 类型的实例构造函数中；

对常量使用静态只读字段：

如果想要声明一个常量，但类型不被支持（不允许）时，使用static readonly可以达到相同的效果。

```
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);
    private byte red, green, blue;
    public Color(byte r, byte g, byte b) {
        red = r;
        green = g;
        blue = b;
    }
}
```

常量和静态只读字段的版本控制：

常量和只读字段具有不同的二进制版本控制语义，常量的值在编译时获得；只读字段的值在运行时获得。

```
using System;
namespace Program1
{
    public class Utils
    {
        public static readonly int X = 1;
    }
}
namespace Program2
{
    class Test
    {
        static void Main() {
            Console.WriteLine(Program1.Utils.X);    //Console.WriteLine打印的值在编译时是未知的
        }
    }
}
```

此例中Program1和Program2表示两个单独编译的程序集，此时Console.WriteLine打印的值在编译时是未知的，如果改变Program1.Utils.X的值，只需重新编译Program1即可；但如果Program1.Utils.X是常量，则必须重新编译Program1和Program2。

## 可变字段

当字段的声明中使用**volatile**修饰符时，该字段为可变字段。

意义？

## 字段初始化

无论是静态字段还是实例字段，字段的初始值都是字段类型的默认值。字段永远不可能是“未初始化”的。

## 变量初始值设定项

对于静态字段，变量初始值设定项相当于在类的初始化的初始化期间执行的赋值语句。

对于实例字段，变量初始值设定项相当于在创建类的实例时执行的赋值语句。

当初始化一个类时，首先将该类中所有的静态字段初始化为字段类型的默认值，然后以文本顺序执行各个静态字段初始值设定项。同理，在创建类的实例时，首先将该类中所有的实例字段初始化为字段类型的默认值，然后以文本顺序执行各个实例字段的初始值设定项。

如果类中存在静态构造函数，则在静态构造函数即将执行之前执行静态字段的初始值设定项；否则将在第一次使用该类时执行静态字段的初始值设定项。实例初始值设定项是在执行类的实例构造函数时立即执行，因此实例字段不能引用正在创建的实例和实例成员，即不能使用this，或者this.x。



