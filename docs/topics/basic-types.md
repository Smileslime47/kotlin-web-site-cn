[//]: # (title: 基本类型)

在 Kotlin 中，所有东西都是对象，在这个意义上讲我们可以在任何变量上调用成员函数与属性。
一些类型可以有特殊的内部表示——例如，数字、字符以及布尔可以<!--
-->在运行时表示为原生类型值，但是对于用户来说，它们看起来就像普通的类。
在本节中，我们会描述 Kotlin 中使用的基本类型：[数字](#数字)、[布尔](#布尔)、
[字符](#字符)、[数组](#数组)与[字符串](#字符串)。

## 数字

### Integer types

Kotlin 提供了一组表示数字的内置类型。
对于整数，有四种不同大小的类型，因此值的范围也不同。

| 类型	 | 大小（比特数）| 最小值 | 最大值 |
|--------|---------------|--------|------- |
| Byte	 | 8             |-128    |127     |
| Short	 | 16            |-32768  |32767   |
| Int	 | 32            |-2,147,483,648 (-2<sup>31</sup>)| 2,147,483,647 (2<sup>31</sup> - 1)|
| Long	 | 64            |-9,223,372,036,854,775,808 (-2<sup>63</sup>)|9,223,372,036,854,775,807 (2<sup>63</sup> - 1)|

所有以未超出 `Int` 最大值的整型值初始化的变量<!--
-->都会推断为 `Int` 类型。如果初始值超过了其最大值，那么推断为 `Long` 类型。
如需显式指定 `Long` 型值，请在该值后追加 `L` 后缀。

```kotlin
val one = 1 // Int
val threeBillion = 3000000000 // Long
val oneLong = 1L // Long
val oneByte: Byte = 1
```

### Floating-point types

对于实数，Kotlin 提供了浮点类型 `Float` 与 `Double` 类型。
根据 [IEEE 754 标准](https://zh.wikipedia.org/wiki/IEEE_754)，
两种浮点类型的*十进制位数*（即可以存储多少位十进制数）不同。
`Float` 反映了 IEEE 754 *单精度*，而 `Double` 提供了*双精度*。
 
| 类型	 | 大小（比特数）| 有效数字比特数 | 指数比特数 | 十进制位数 |
|--------|---------------|--------------- |------------|------------|
| Float	 | 32            |24              |8           |6-7         |
| Double | 64            |53              |11          |15-16       |    
  
You can initialize `Double` and `Float` variables  with numbers having a fractional part.
It's separated from the integer part by a period (`.`)
对于以小数初始化的变量，编译器会推断为 `Double` 类型。

```kotlin
val pi = 3.14 // Double
// val one: Double = 1 // Error: type mismatch
val oneDouble = 1.0 // Double
```

如需将一个值显式指定为 `Float` 类型，请添加 `f` 或 `F` 后缀。
如果这样的值包含多于 6～7 位十进制数，那么会将其舍入。

```kotlin
val e = 2.7182818284 // Double
val eFloat = 2.7182818284f // Float，实际值为 2.7182817
```

请注意，与一些其他语言不同，Kotlin 中的数字没有隐式拓宽转换。
例如，具有 `Double` 参数的函数只能对 `Double` 值调用，而不能对 `Float`、
`Int` 或者其他数字值调用。

```kotlin
fun main() {
    fun printDouble(d: Double) { print(d) }

    val i = 1    
    val d = 1.0
    val f = 1.0f 

    printDouble(d)
//    printDouble(i) // 错误：类型不匹配
//    printDouble(f) // 错误：类型不匹配
}
```

如需将数值转换为不同的类型，请使用[显式转换](#显式转换)。

### 字面常量

数值常量字面值有以下几种:

* 十进制: `123`
  * Long 类型用大写 `L` 标记: `123L`
* 十六进制: `0x0F`
* 二进制: `0b00001011`

>不支持八进制。
>
{type="note"}

Kotlin 同样支持浮点数的常规表示方法:
 
* 默认 double：`123.5`、`123.5e10`
* Float 用 `f` 或者 `F` 标记: `123.5f`
 
你可以使用下划线使数字常量更易读：

```kotlin
val oneMillion = 1_000_000
val creditCardNumber = 1234_5678_9012_3456L
val socialSecurityNumber = 999_99_9999L
val hexBytes = 0xFF_EC_DE_5E
val bytes = 0b11010010_01101001_10010100_10010010
```

### Numbers representation on the JVM

On the JVM platform, numbers are stored as primitive types: `int`, `double`, and so on. 
Exceptions are cases when you create a nullable number reference such as `Int?` or use generics.
In these cases numbers are boxed in Java clases `Integer`, `Double`, and so on.

Note that nullable references to the same number can be different objects:

```kotlin
fun main() {
//sampleStart
    val a: Int = 100
    val boxedA: Int? = a
    val anotherBoxedA: Int? = a
    
    val b: Int = 10000
    val boxedB: Int? = b
    val anotherBoxedB: Int? = b
    
    println(boxedA === anotherBoxedA) // true
    println(boxedB === anotherBoxedB) // false
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

另一方面，它们仍然相等:

```kotlin
fun main() {
//sampleStart
    val a: Int = 10000
    println(a == a) // 输出“true”
    val boxedA: Int? = a
    val anotherBoxedA: Int? = a
    println(boxedA == anotherBoxedA) // 输出“true”
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

### 显式转换

由于不同的表示方式，较小类型并*不是*较大类型的子类型。
如果它们是的话，就会出现下述问题：

```kotlin
// 假想的代码，实际上并不能编译：
val a: Int? = 1 // 一个装箱的 Int (java.lang.Integer)
val b: Long? = a // 隐式转换产生一个装箱的 Long (java.lang.Long)
print(b == a) // 惊！这将输出“false”鉴于 Long 的 equals() 会检测另一个是否也为 Long
```

所以会悄无声息地失去相等性，更别说同一性了。

因此较小的类型***不能**隐式转换*为较大的类型。
这意味着把 `Byte` 型值赋给一个 `Int` 变量必须显式转换。

```kotlin
fun main() {
//sampleStart
    val b: Byte = 1 // OK, 字面值会静态检测
    // val i: Int = b // 错误
    val i1: Int = b.toInt()
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

All number types support conversions to other types:

* `toByte(): Byte`
* `toShort(): Short`
* `toInt(): Int`
* `toLong(): Long`
* `toFloat(): Float`
* `toDouble(): Double`
* `toChar(): Char`

缺乏隐式类型转换很少会引起注意，因为类型会从上下文推断出来，
而算术运算会有重载做适当转换，例如：

```kotlin
val l = 1L + 3 // Long + Int => Long
```

### 运算

Kotlin支持数字运算的标准集：`+`、 `-`、 `*`、 `/`、 `%`。它们被定义<!--
-->为相应的类成员。

```kotlin
fun main() {
//sampleStart
    println(1 + 2)
    println(2_500_000_000L - 1L)
    println(3.14 * 2.71)
    println(10.0 / 3)
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

You can also override these operators for custom classes. See [Operator overloading](operator-overloading.md) for details.

#### 整数除法

整数间的除法总是返回整数。会丢弃任何小数部分。

```kotlin
fun main() {
//sampleStart
    val x = 5 / 2
    //println(x == 2.5) // ERROR: Operator '==' cannot be applied to 'Int' and 'Double'
    println(x == 2)
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

对于任何两个整数类型之间的除法来说都是如此。

```kotlin
fun main() {
//sampleStart
    val x = 5L / 2
    println(x == 2L)
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

如需返回浮点类型，请将其中的一个参数显式转换为浮点类型。

```kotlin
fun main() {
//sampleStart
    val x = 5 / 2.toDouble()
    println(x == 2.5)
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

#### 位运算

Kotlin provides a set of _bitwise operations_ on integer numbers. They operate on the binary level directly with 
bits of the numbers' representation.
Bitwise operations are represented by functions that can be called in infix form. They can be applied only to `Int` and `Long`.

```kotlin
val x = (1 shl 2) and 0x000FF000
```

这是完整的位运算列表：

* `shl(bits)` – 有符号左移
* `shr(bits)` – 有符号右移
* `ushr(bits)` – 无符号右移
* `and(bits)` – 位**与**
* `or(bits)` – 位**或**
* `xor(bits)` – 位**异或**
* `inv()` – 位非

### 浮点数比较

本节讨论的浮点数操作如下：

* 相等性检测：`a == b` 与 `a != b`
* 比较操作符：`a < b`、 `a > b`、 `a <= b`、 `a >= b`
* 区间实例以及区间检测：`a..b`、 `x in a..b`、 `x !in a..b`

当其中的操作数 `a` 与 `b` 都是静态已知的 `Float` 或 `Double` 或者它们对应的可空类型（声明为<!--
-->该类型，或者推断为该类型，或者[智能类型转换](typecasts.html#智能转换)的结果是该类型），两数字所形成的操作<!--
-->或者区间遵循 [IEEE 754 浮点运算标准](https://zh.wikipedia.org/wiki/IEEE_754)。

然而，为了支持泛型场景并提供全序支持，当这些操作数**并非**静态类型为<!--
-->浮点数（例如是 `Any`、 `Comparable<……>`、 类型参数）时，这些操作使用<!--
-->为 `Float` 与 `Double` 实现的不符合标准的 `equals` 与 `compareTo`，这会出现：

* 认为 `NaN` 与其自身相等
* 认为 `NaN` 比包括正无穷大（`POSITIVE_INFINITY`）在内的任何其他元素都大
* 认为 `-0.0` 小于 `0.0`

### 无符号整型

>无符号类型自 Kotlin 1.3 起才可用，并且目前处于 [Beta](components-stability.md) 版。详见[下文](#无符号整数的-beta-状态)
>
{type="note"}

In addition to [integer types](#integer-types), Kotlin provides the following types for unsigned integer numbers:

* `UByte`: 无符号 8 比特整数，范围是 0 到 255
* `UShort`: 无符号 16 比特整数，范围是 0 到 65535
* `UInt`: 无符号 32 比特整数，范围是 0 到 2^32 - 1
* `ULong`: 无符号 64 比特整数，范围是 0 到 2^64 - 1

无符号类型支持其对应有符号类型的大多数操作。

>将类型从无符号类型更改为对应的有符号类型（反之亦然）是*二进制不兼容*变更。
>
{type="note"}

无符号类型是使用尚未稳定特性（即[内联类](inline-classes.md)）实现的。

#### Unsigned arrays and ranges 

与原生类型相同，每个无符号类型都有表示相应类型数组的类型：

* `UByteArray`: 无符号字节数组
* `UShortArray`: 无符号短整型数组
* `UIntArray`: 无符号整型数组
* `ULongArray`: 无符号长整型数组

与有符号整型数组一样，它们提供了类似于 `Array` 类的 API 而没有装箱开销。

此外，[区间与数列](ranges.md)也支持 `UInt` 与 `ULong`（通过这些类 `UIntRange`、
`UIntProgression`、 `ULongRange`、 `ULongProgression`）

#### 字面值

为使无符号整型更易于使用，Kotlin 提供了用后缀标记整型字面值来<!--
-->表示指定无符号类型（类似于 `Float` 或 `Long`）：

* u` 与 `U` 将字面值标记为无符号。 The exact type is determined based on the expected type.
If no expected type is provided, compiler will use `UInt` or `ULong` depending on the size of literal.

```kotlin
val b: UByte = 1u  // UByte，已提供预期类型
val s: UShort = 1u // UShort，已提供预期类型
val l: ULong = 1u  // ULong，已提供预期类型

val a1 = 42u // UInt：未提供预期类型，常量适于 UInt
val a2 = 0xFFFF_FFFF_FFFFu // ULong：未提供预期类型，常量不适于 UInt
```

* `uL` 与 `UL` 显式将字面值标记为无符号长整型。

```kotlin
val a = 1UL // ULong，即使未提供预期类型并且常量适于 UInt
```

#### 无符号整数的 beta 状态

无符号类型的设计还是 [Beta](components-stability.md) 版，这意味着其兼容性仅是尽力而为，不能保证。

使用无符号算术时，会报一个警告，提示该特性尚未稳定发布。
如需消除警告，必须选择加入对无符号类型的使用：

* 如需传播选择加入要求，请以 `@ExperimentalUnsignedTypes` 标注使用了无符号整型的声明。
* 如需选择加入而不传播，要么使用 `@OptIn(ExperimentalUnsignedTypes::class)` 注解标注声明，
要么将 `-Xopt-in=kotlin.ExperimentalUnsignedTypes` 传给编译器。

你的客户是否必须选择使用你的 API 取决于你，不过请记住，
无符号整型是一个非稳定特性，因此使用它们的 API 可能会因语言的变更而发生突然破坏。 

See the [opt-in requirements](opt-in-requirements.md) for details on using APIs that require opt-in.

#### 深入探讨

关于技术细节与深入探讨<!--
-->请参见[无符号类型的语言提案](https://github.com/Kotlin/KEEP/blob/master/proposals/unsigned-types.md)。

## 布尔

The type `Boolean` represents boolean objects that can have two values: `true` and `false`.

`Boolean` has a nullable counterpart `Boolean?` that also has the `null` value.

Built-in operations on booleans include:

* `||` – disjunction (logical _OR_)
* `&&` – conjunction (logical _AND_)
* `!` - negation (logical _NOT_)

`||` and `&&` work lazily.

```kotlin
fun main() {
//sampleStart
    val myTrue: Boolean = true
    val myFalse: Boolean = false
    val boolNull: Boolean? = null
    
    println(myTrue || myFalse)
    println(myTrue && myFalse)
    println(!myTrue)
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

>**On JVM**: nullable references to boolean objects are boxed similarly [numbers](#numbers-representation-on-the-jvm).
>
{type="note"}

## 字符

字符用 `Char` 类型表示。 字符字面值用单引号括起来: `'1'`。

特殊字符可以以转义反斜杠 `\` 开始。
支持这几个转义序列：`\t`、 `\b`、`\n`、`\r`、`\'`、`\"`、`\\` 与 `\$`。

编码其他字符要用 Unicode 转义序列语法：`'\uFF00'`。

```kotlin
fun main() {
//sampleStart
    val aChar: Char = 'a'
 
    println(aChar)
    println('\n') //prints an extra newline character
    println('\uFF00')
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

If a value of character variable is a digit, 可以显式将其转换为 `Int` 数字：

```kotlin
fun decimalDigitValue(c: Char): Int {
    if (c !in '0'..'9')
        throw IllegalArgumentException("Out of range")
    return c.toInt() - '0'.toInt() // 显式转换为数字
}
```

>**On JVM**: Like [numbers](#numbers-representation-on-the-jvm), characters are boxed when a nullable reference is needed.
>Identity is not preserved by the boxing operation.
>
{type="note"}

## 字符串

Kotlin 中字符串用 `String` 类型表示。 Generally, a string value is a sequence of characters in double quotes (`"`).
 
```kotlin
val str = "abcd 123"
```

字符串的元素——字符可以使用索引运算符访问: `s[i]`。
You can iterate over these characters with a `for` loop:

```kotlin
fun main() {
val str = "abcd"
//sampleStart
for (c in str) {
    println(c)
}
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

字符串是不可变的。Once you initialize a string, you can't change its value or assign a new value to it.
All operations that transform strings return their results in a new `String` object, leaving the original string unchanged.

```kotlin
fun main() {
//sampleStart
    val str = "abcd"
    println(str.toUpperCase()) // Create and print a new String object
    println(str) // the original string remains the same
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

如需连接字符串，可以用 `+` 操作符。这也适用于连接字符串与其他类型的值，
只要表达式中的第一个元素是字符串：

```kotlin
fun main() {
//sampleStart
val s = "abc" + 1
println(s + "def")
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

请注意，在大多数情况下，优先使用[字符串模板](#字符串模板)或原始字符串而不是字符串连接。

### 字符串字面值

Kotlin 有两种类型的字符串字面值:

* *转义*字符串可以包含转义字符
* *原始*字符串可以包含换行以及任意文本

以下是转义字符串的一个示例：

```kotlin
val s = "Hello, world!\n"
```

转义采用传统的反斜杠（`\`）方式。参见上面的 [字符](#字符) 查看支持的转义序列。

*原始字符串* 使用三个引号（`"""`）分界符括起来，内部没有转义并且可以包含换行以及任何其他字符:

```kotlin
val text = """
    for (c in "foo")
        print(c)
"""
```

To remove leading whitespace from raw strings, use the [`trimMargin()`](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/trim-margin.html) function:

```kotlin
val text = """
    |Tell me and I forget.
    |Teach me and I remember.
    |Involve me and I learn.
    |(Benjamin Franklin)
    """.trimMargin()
```

默认 `|` 用作边界前缀，但你可以选择其他字符并作为参数传入，比如 `trimMargin(">")`。

### 字符串模板

字符串字面值可以包含*模板表*达式——一些小段代码，会求值并把结果合并到字符串中。
模板表达式以美元符（`$`）开头，要么由一个的名称构成:

```kotlin
fun main() {
//sampleStart
    val i = 10
    println("i = $i") // 输出“i = 10”
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

要么是用花括号括起来的表达式:

```kotlin
fun main() {
//sampleStart
    val s = "abc"
    println("$s.length is ${s.length}") // 输出“abc.length is 3”
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

You can use templates both in raw and escaped strings.
To insert the `$` character in a raw string (which doesn't support backslash escaping), use the following syntax:

```kotlin
val price = """
${'$'}9.99
"""
```

## Arrays

数组在 Kotlin 中使用 `Array` 类来表示。它定义了 `get` 与 `set` 函数（按照运算符重载约定这会转变为 `[]`）<!--
-->与 `size` 属性及其他有用的成员函数：

```kotlin
class Array<T> private constructor() {
    val size: Int
    operator fun get(index: Int): T
    operator fun set(index: Int, value: T): Unit

    operator fun iterator(): Iterator<T>
    // ……
}
```

可以使用函数 `arrayOf()` 来创建一个数组并传递元素值给它，这样 `arrayOf(1, 2, 3)` 创建了 array `[1, 2, 3]`。
或者，函数 `arrayOfNulls()` 可以用于创建一个指定大小的、所有元素都为空的数组。

另一个选项是用接受数组大小以及一个函数参数的 `Array` 构造函数，用作参数的函数能够返回<!--
-->给定索引的元素：

```kotlin
fun main() {
//sampleStart
    // 创建一个 Array<String> 初始化为 ["0", "1", "4", "9", "16"]
    val asc = Array(5) { i -> (i * i).toString() }
    asc.forEach { println(it) }
//sampleEnd
}
```
{kotlin-runnable="true" kotlin-min-compiler-version="1.3"}

如上所述，`[]` 运算符代表调用成员函数 `get()` 与 `set()`。

Kotlin 中数组是*不型变的（invariant）*。这意味着 Kotlin 不让我们把 `Array<String>`
赋值给 `Array<Any>`，以防止可能的运行时失败（但是你可以使用 `Array<out Any>`,
参见[类型投影](generics.md#类型投影)）。

### 原生类型数组

Kotlin 也有无装箱开销的类来表示原生类型数组: `ByteArray`、
`ShortArray`、`IntArray` 等等。这些类与 `Array` 并没有继承关系，但是<!--
-->它们有同样的方法属性集。它们也都有相应的工厂方法:

```kotlin
val x: IntArray = intArrayOf(1, 2, 3)
x[0] = x[1] + x[2]
```

```kotlin
// 大小为 5、值为 [0, 0, 0, 0, 0] 的整型数组
val arr = IntArray(5)

// 例如：用常量初始化数组中的值
// 大小为 5、值为 [42, 42, 42, 42, 42] 的整型数组
val arr = IntArray(5) { 42 }

// 例如：使用 lambda 表达式初始化数组中的值
// 大小为 5、值为 [0, 1, 2, 3, 4] 的整型数组（值初始化为其索引值）
var arr = IntArray(5) { it * 1 } 
```