# 变量

一个有效的变量名由字母或者下划线开头，后面跟上任意数量的字母，数字，或者下划线。按照正常的正则表达式，它将被表述为：'[a-zA-Z_\x7f-\xff][a-zA-Z0-9_\x7f-\xff]*’

#### note:

* Note: 在此所说的字母是 a-z，A-Z，以及 ASCII 字符从 127 到 255（0x7f-0xff）。
* Note: *$this* 是一个特殊的变量，它不能被赋值。

# 常量

常量名和其它任何 PHP 标签遵循同样的命名规则。合法的常量名以字母或下划线开始，后面跟着任何字母，数字或下划线。用正则表达式是这样表达的：[a-zA-Z_\x7f-\xff][a-zA-Z0-9_\x7f-\xff]*

# 表达式

# 运算符

# 运算符优先级
#### note:

Note:尽管 = 比其它大多数的运算符的优先级低，PHP 仍旧允许类似如下的表达式：if (!$a = foo())，在此例中 foo() 的返回值被赋给了 $a。

# 算术运算符

除法运算符总是返回浮点数。只有在下列情况例外：两个操作数都是整数（或字符串转换成的整数）并且正好能整除，这时它返回一个整数。

取模运算符的操作数在运算之前都会转换成整数（除去小数部分）
#### note:

Note: 取模 $a % $b 在 $a 为负值时的结果也是负值

`every string will be converted to 0.`

* echo "foo" * "bar”;    // 0
* echo "foo" / "bar”;   // Warning: Division by zero in /tmp/test.php on line 3

# 赋值运算符

注意赋值运算将原变量的值拷贝到新变量中（传值赋值），所以改变其中一个并不影响另一个。这也适合于在很密集的循环中拷贝一些值例如大数组。
也可以使用引用赋值，用 $var = &$othervar; 语法。引用赋值意味着两个变量都指向同一个数据，没有任何数据的拷贝
在 PHP 5中，对象总是通过引用赋值的，除非明确使用新的 clone关键字。

# 位运算符

位运算符允许对整型数中指定的位进行置位。如果左右参数都是字符串，则位运算符将操作字符的 ASCII 值。
Warning：在 32 位系统上不要右移超过 32 位。不要在结果可能超过 32 位的情况下左移

# 比较运算符

如果比较一个整数和字符串，则**字符串会被转换为整数**。如果比较两个数字字符串，则作为整数比较。
##### 比较多种类型
运算数 1 类型	 | 运算数 1 类型	| 结果
----------- | ----------------- | --------------------
null 或 string |	string |	将 NULL 转换为 ""，进行数字或词汇比较
bool 或 null |	任何其它类型 |	转换为 bool，FALSE < TRUE
object |	object	| 内置类可以定义自己的比较，不同类不能比较，相同类和数组同样方式比较属性（PHP 4 中），PHP 5 有其自己的说明
string，resource或 number |	string，resource或 number |	将字符串和资源转换成数字，按普通数学比较
array |	array |	具有较少成员的数组较小，如果运算数 1 中的键不存在于运算数 2 中则数组无法比较，否则挨个值比较（见下例）
array |	任何其它类型	| array 总是更大
object | 任何其它类型	 | object 总是更大

#### note:

Note: 注意三元运算符是个语句，因此其求值不是变量，而是语句的结果。如果想通过引用返回一个变量这点就很重要。在一个通过引用返回的函数中语句 return $var == 42 ? $a : $b; 将不起作用，以后的 PHP 版本会为此发出一条警告。

错误控制运算符

Note: @ 运算符只对表达式有效。对新手来说一个简单的规则就是：如果能从某处得到值，就能在它前面加上 @ 运算符。例如，可以把它放在变量，函数和 include() 调用，常量，等等之前。不能把它放在函数或类的定义之前，也不能用于条件结构例如 if 和 foreach 等

# 执行运算符

PHP 支持一个执行运算符：反引号（\`\`）。注意这不是单引号！PHP 将尝试将反引号中的内容作为外壳命令来执行，并将其输出信息返回（例如，可以赋给一个变量而不是简单地丢弃到标准输出）。使用反引号运算符“`”的效果与函数 shell_exec() 相同。

#### note:

Note: 反引号运算符在激活了安全模式或者关闭了 shell_exec() 时是无效的

# 递增／递减运算符
**Note**: 递增／递减运算符不影响布尔值。递减 NULL 值也没有效果，但是递增 NULL 的结果是 1。

`在处理字符变量的算数运算时，PHP 沿袭了 Perl 的习惯，而非 C 的。例如，在 Perl 中 'Z'+1 将得到 'AA'，而在 C 中，'Z'+1 将得到 '['（ord('Z') == 90，ord('[') == 91）。注意字符变量只能递增，不能递减，并且只支持纯字母（a-z 和 A-Z）。`

# 逻辑运算符

# 字符串运算符

# 数组运算符
> \+ 运算符把右边的数组元素（**除去键值与左边的数组元素相同的那些元素**）附加到左边的数组后面，但是重复的键值不会被覆盖。

# 类型运算符
1. instanceof 用于确定一个 PHP 变量是否属于某一类 class 的实例
2. instanceof 也可用来确定一个变量是不是继承自某一父类的子类的实例
3. instanceof也可用于确定一个变量是不是实现了某个接口的对象的实例

`Note: instanceof 通常直接与类名一起使用，但也可以使用对象或字符串变量`

然而 instanceof 的使用还有一些陷阱必须了解。在 PHP 5.1.0之前，如果要检查的类名称不存在，instanceof 会调用 __autoload()。另外，如果该类没有被装载则会产生一个致命错误。可以通过使用动态类引用(dynamic class reference)或用一个包含类名的字符串变量来避开这种问题.

instanceof 运算符是 PHP 5 引进的。在此之前用 is_a()，但是 is_a() 已经过时了，最好用 instanceof。

