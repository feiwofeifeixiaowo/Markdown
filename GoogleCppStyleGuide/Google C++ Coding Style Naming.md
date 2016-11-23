### Google C++ Style Guide

- Naming
    - General Naming Rules
    - File Names
    - Type Names
    - Variable Names
    - Constant Names
    - Function Names
    - Namespace Names
    - Enumerator Names
    - Macro Names
    - Exceptions to Naming Rules
----
Tips:
1. 函数命名，变量命名，文件命名要有描述性；少用缩写。

```cpp
int price_count_reader;
int num_errors;
int num_dns_connections;
```

2. 文件名要全部小写，可以包含下划线(_)或连字符(-).

> C++ 文件以.cc 结尾，头文件以.h 结尾。专门插入文本的文件以.inc 结尾

```cpp
my_useful_class.cc  // 感觉这种好点
my-useful-class.cc  // 感觉这种好点+1
myusefeulclass.cc
muusefulclass_test.cc
```
3. 类型名称的每个单词首字母均大写，不包含下划线：MyExcitingClass,MyExcitingEnum.

> 所有的类型命名 ---- 类、结构体、类型定义(typedef)、枚举 ---- 均使用相同的约定。

```cpp
// classes and structs
class UrlTable { ...
class UrlTableTester { ...
struct UrlTableProperties { ...

// typedefs
typedef hash_map<UrlTableProperties *, string> PropertiesMap;

// enums
enum UrlTableErrors { ...
```

4. 变量名一律小写，单词之间用下划线连接。类的成员变量以下划线结尾，但是结构体的就不用。如：

```cpp
a_local_variable;
a_struct_data_member;
a_class_data_member;

// 普通变量名
string table_name;
string tablename;

// 不推荐
string tableName;

// 类数据成员: 不管是静态还是非静态，类的数据成员后要接下划线。
class TableInfo {
    ...
private:
    string table_name_;
    static Pool<TableInfo>* pool_;
}

// 结构体变量: 跟普通变量一样，不需要像类数据成员一样加下划线
struct UrlTableProperties {
    string name;
    int num_entries;
}

// 全局变量：少用全局变量，可以用g_ 标识作为前缀，以便更好的区分局部变量
```

5. 常量名称前加k，且除去开头的k以外每个单词开头字母均大写。

```cpp
const int kDaysInAWeek = 7;
```

6. 函数命名

> 1. 常规函数： 函数名的每个单词首字母大写，没有下划线。

```cpp
AddTableEntry();
DeleteUrl();

// 如果某个函数出错时直接crash，就在函数名加上OrDie
OpenFileOrDie();
```
> 2. 取值和设值函数： 函数要与存取的变量名匹配。

```cpp
class MyClass {
    public:
    ...
    int num_entries() const { return num_entries_; }
    void set_num_entries(int num_entries) { num_entries_ = num_entries; }
    private:
    int num_entries_;
};

```

7. 命名空间命名： 用小写字幕命名，并基于项目名称和目录结构： google_awesome_project.

8. 枚举命名： 与常量一致或与宏一致。如：kEnumName 或 ENUM_NAME

```cpp
// 推荐
enum UrlTableErrors {
  kOK = 0,
  kErrorOutOfMemory,
  kErrorMalformedInput,
};

// 可以但不推荐
enum AlternativeUrlTableErrors {
    OK = 0,
    OUT_OF_MEMORY = 1,
    MALFORMED_INPUT = 2,
};

```

9. 宏命名：MY_MACRO_THAT_SCARES_SMALL_CHILDREN

> Google 不推荐使用宏。

```cpp
#define ROUND(x) ...
#define PI_ROUNDED 3.0
```

10. 命名规则的特例


