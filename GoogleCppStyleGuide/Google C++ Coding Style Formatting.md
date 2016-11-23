### Google C++ Style Guide

- Formatting
    - Line Length
    - Non-ASCII Characters
    - Spaces vs. Tabs
    - Function Declarations and Definitions
    - Lambda Expressions
    - Function Calls
    - Braced Initializer List Format
    - Conditionals
    - Loops and Switch Statements
    - Pointer and Reference Expressions
    - Boolean Expressions
    - Return Values
    - Variable and Array Initialization
    - Preprocessor Directives
    - Class Format
    - Constructor Initializer Lists
    - Namespace Formatting
    - Horizontal Whitespace
    - Vertical Whitespace
----
Tips:

> 代码风格和格式确实比较随意, 但一个项目中所有人遵循同一风格是非常容易的. 个体未必同意下述每一处格式规则, 但整个项目服从统一的编程风格是很重要的, 只有这样才能让所有人能很轻松的阅读和理解代码.

1. 行长度：每一行代码字符数不超过80.

    - 如果一行注释包含了超过 80 字符的命令或 URL, 出于复制粘贴的方便允许该行超过 80 字符.
    - 包含长路径的 #include 语句可以超出80列. 但应该尽量避免.
    - 头文件保护 可以无视该原则.

2. 非ASCII字符：尽量不使用非ASCII字符，使用时必须使用UTF-8

3. 空格还是制表位：只使用空格，每次缩进2个空格。

4. 函数声明与定义：返回类型和函数名在同一行, 参数也尽量放在同一行，如果放不下就对形参分行。

    - 如果返回类型和函数名在一行放不下，分行。
    - 如果返回类型那个与函数声明或定义分行了，不要缩进。
    - 左圆括号总是和函数名在同一行;
    - 函数名和左圆括号间没有空格;
    - 圆括号与参数间没有空格;
    - 左大括号总在最后一个参数同一行的末尾处;
    - 如果其它风格规则允许的话，右大括号总是单独位于函数最后一行，或者与左大括号同一行。
    - 右大括号和左大括号间总是有一个空格;
    - 函数声明和定义中的所有形参必须有命名且一致;
    - 所有形参应尽可能对齐;
    - 缺省缩进为 2 个空格;
    - 换行后的参数保持 4 个空格的缩进;


```cpp
// 推荐
ReturnType ClassName::FunctionName(Type par_name1, Type par_name2) {
    DoSomething();
    ...
}

// 太长了可以这样分行
ReturnType ClassName::ReallyLongFunctionName(Type par_name1, Type par_name2,
                                             Type par_name3) {
    DoSomething();
    ...
}

```
5. Lambda 表达式

> 其它函数怎么格式化形参和函数体，Lambda 表达式就怎么格式化；捕获列表同理。

> 若用引用捕获，在变量名和 & 之间不留空格。

```cpp
int x = 0;
auto add_to_x = [&x](int n) { x += n; };
```

6. 函数调用

> 要么一行写完函数调用，要么在圆括号里对参数分行，要么参数另起一行且缩进四格。如果没有其它顾虑的话，尽可能精简行数，比如把多个参数适当地放在同一行里。

```cpp

// 参数列表尽量放在同一行
bool retval = DoSomething(argument1, argument2, argument3);

// 当然，太长了也可以分割开
bool retval = DoSomething(averyveryveryverylongargument1,
                          argument2, argument3);
                          

if (...) {
  ...
  ...
  if (...) {
    DoSomething(
        argument1, argument2,  // 4 空格缩进
        argument3, argument4);
  }
  
// 有些形参比较复杂，可以定义局部变量提升可读性
int my_heuristic = scores[x] * y + bases[x];
bool retval = DoSomething(my_heuristic, x, y, z);

// 有些形参比较复杂，可以加注释说明
bool retval = DoSomething(scores[x] * y + bases[x],  // Score heuristic.
                          x, y, z);
                          
                          
// 通过 3x3 矩阵转换 widget.
my_widget.Transform(x1, x2, x3,
                    y1, y2, y3,
                    z1, z2, z3);
```

7. 列表初始化格式：平时怎么格式化函数调用就怎么格式化

8. 条件语句：倾向于不在圆括号内使用空格。关键字if else 另起一行

```cpp
if (condition) {  圆括号里没空格紧邻。
  ...  // 2 空格缩进。
} else {  // else 与 if 的右括号同一行。
  ...

if (x == kFoo) return new Foo();
if (x == kBar) return new Bar();

// 只要其中一个分支用了大括号，两个分支都要用上大括号。
if (condition) {
  foo;
} else {
  bar;
}


```
9. 循环和switch语句

> switch 语句可以使用大括号分段，以表明 cases 之间不是连在一起的。在单语句循环里，括号可用可不用。空循环体应使用 {} 或 continue.

```cpp
// 如果有不满足 case 条件的枚举值, switch 应该总是包含一个 default 匹配 (如果有输入值没有 case 去处理, 
// 编译器将报警). 如果 default 应该永远执行不到, 简单的加条 assert:

switch (var) {
  case 0: {  // 2 空格缩进
    ...      // 4 空格缩进
    break;
  }
  case 1: {
    ...
    break;
  }
  default: {
    assert(false);
  }
}


// 单语句循环里，括号可用可不用：
for (int i = 0; i < kSomeNumber; ++i)
    printf("I love you\n");


// 空循环体应使用 {} 或 continue, 而不是一个简单的分号.
while (condition) {
  // 反复循环直到条件失效。
}
for (int i = 0; i < kSomeNumber; ++i) {}  // 可 - 空循环体。
while (condition) continue;  // 可 - contunue 表明没有逻辑。

```
10. 指针和引用表达式：句点或箭头前后不要有空格。指针/地址操作符(*, &) 之后不能有空格。

```cpp
// 指针和引用表达式的正确使用
x = *p;
p = &x;
x = r.y;
x = r->y;

// 空格前置
char *c;
const string &str;

// 空格后置  选择这个
char* c;    // 但是别忘记了 char* c, *d, *e, ...;
const string& str;

```

11. 布尔表达式：如果布尔表达式超长了（80字符），断行方式需要统一

```cpp
// && 总是位于行尾
if (this_one_thing > this_other_thing &&
    a_third_thing == a_fourth_thing &&
    yet_another & last_one) {
  ...
}

```

12. 函数返回值：return 表达式里没必要都用圆括号

13. 变量及数组初始化

> 请务必小心列表初始化 {...} 用 std::initializer_list 构造函数初始化出的类型。非空列表初始化就会优先调用 std::initializer_list, 不过空列表初始化除外，后者原则上会调用默认构造函数。为了强制禁用 std::initializer_list 构造函数，请改用括号。

> 列表初始化不允许整型类型的四舍五入，这可以用来避免一些类型上的编程失误。

```cpp
// 您可以用 =, () 和 {}, 以下都对：
int x = 3;
int x(3);
int x{3};
string name("Some Name");
string name = "Some Name";
string name{"Some Name"};

```
14. 预处理指令：预处理指令不要缩进, 从行首开始.

```cpp
// 可 - directives at beginning of line
  if (lopsided_score) {
#if DISASTER_PENDING      // 正确 -- 行开头起。
    DropEverything();
#endif
    BackToNormal();
  }

```

15. 类格式：访问控制块的声明依次序是 public:, protected:, private:, 每次缩进 1 个空格.

    - 所有基类名应在 80 列限制下尽量与子类名放在同一行.
    - 关键词 public:, protected:, private: 要缩进 1 个空格.
    - 除第一个关键词 (一般是 public) 外, 其他关键词前要空一行. 如果类比较小的话也可以不空.
    - 这些关键词后不要保留空行.
    - public 放在最前面, 然后是 protected, 最后是 private.
    

```cpp
class MyClass : public OtherClass {
 public:      // 注意有 1 空格缩进!
  MyClass();  // 照常，2 空格缩进。
  explicit MyClass(int var);
  ~MyClass() {}

  void SomeFunction();
  void SomeFunctionThatDoesNothing() {
  }

  void set_some_var(int var) { some_var_ = var; }
  int some_var() const { return some_var_; }

 private:
  bool SomeInternalFunction();

  int some_var_;
  int some_other_var_;
  DISALLOW_COPY_AND_ASSIGN(MyClass);
};
```

16. 构造函数初始值列表：放在同一行或按四格缩进并排

```cpp
// 当全放在一行合适时：
MyClass::MyClass(int var) : some_var_(var), some_other_var_(var + 1) {
或

// 如果要断成多行，缩进四格，冒号放在第一行初始化句：
MyClass::MyClass(int var)
    : some_var_(var),             // 4 空格缩进
      some_other_var_(var + 1) {  // 对准
  ...
  DoSomething();
  ...
}

```

17. 命名空间格式化：命名空间内容不缩进

```cpp
namespace {
void foo() {  // 正确。命名空间内没有额外的缩进。
  ...
}

}  // namespace
```

18. 水平留白：不要在行尾添加没有意义的留白

```cpp
void f(bool b) {  // 左大括号前恒有空格。
  ...
int i = 0;  // 分号前不加空格。
int x[] = {0};
// 继承与初始化列表中的冒号前后恒有空格。
class Foo : public Bar {
 public:
  // 至于内联函数实现，在大括号内部加上空格并编写实现。
  Foo(int b) : Bar(), baz_(b) {}  // 大括号里面是空的话，不加空格。
  void Reset() { baz_ = 0; }  // 用括号把大括号与实现分开。
  ...
  

// 循环和条件
if (b) {          // if 条件语句和循环语句关键字后均有空格。
} else {          // else 前后有空格。
}
while (test) {}   // 圆括号内部不紧邻空格。
switch (i) {
for (int i = 0; i < 5; ++i) {
for ( ; i < 5 ; ++i) {  // 循环里内 ; 后恒有空格，； 前可以加个空格。
switch (i) {
  case 1:         // switch case 的冒号前无空格。
    ...
  case 2: break;  // 如果冒号有代码，加个空格。
  
// 操作符
// 赋值操作系统前后恒有空格。
x = 0;

// 其它二元操作符也前后恒有空格，不过对 factors 前后不加空格也可以。
// 圆括号内部不紧邻空格。
v = w * x + y / z;
v = w * (x + z);

// 在参数和一元操作符之间不加空格。
x = -5;
++x;
if (x && !y)
  ...
  
// 模板和转换
// 尖叫括号(< and >) 不与空格紧邻，< 前没有空格，>( 之间也没有。
vector<string> x;
y = static_cast<char*>(x);

// 在类型与指针操作符之间留空格也可以，但要保持一致。
vector<char *> x;
set<list<string>> x;        // 在 C++11 代码里可以这样用了。
set<list<string> > x;       // C++03 中要在 > > 里留个空格。

// [个人不推荐]您或许可以在 < < 里加上一对对称的空格。
set< list<string> > x;
```

19. 垂直留白：越少越好

> 这不仅仅是规则而是原则问题了: 不在万不得已, 不要使用空行. 尤其是: 两个函数定义之间的空行不要超过 2 行, 函数体首尾不要留空行, 函数体中也不要随意添加空行.

> 基本原则是: 同一屏可以显示的代码越多, 越容易理解程序的控制流. 当然, 过于密集的代码块和过于疏松的代码块同样难看, 取决于你的判断. 但通常是垂直留白越少越好.

空行心得如下：
- 函数体内开头或结尾的空行可读性微乎其微。
- 在多重 if-else 块里加空行或许有点可读性。


