### Google C++ Style Guide

- Comments
    - Comment Style
    - File Comments
    - Class Comments
    - Function Comments
    - Variable Comments
    - Implementation Comments
    - Punctuation, Spelling and GrammarTODO Comments
    - Deprecation Comments
----
Tips:
1. 陈硕大大推荐使用// 风格注释

2. 文件注释

> 1. 版权声明(Copyright 2008 Google Inc.)

> 2. 许可证（Apache 2.0, BSD, LGPL, GPL）

> 3. 作者信息：标识文件的原始作者

> 4. 描述文件内容。在.h 文件要对所声明的类的功能和用法作简单说明.

3. 类注释

> 每个类的定义都要附带一份注释，描述类的功能与用法。

```cpp
// Iterates over the contents of a GargantuanTable.  Sample usage:
//    GargantuanTable_Iterator* iter = table->NewIterator();
//    for (iter->Seek("foo"); !iter->done(); iter->Next()) {
//      process(iter->key(), iter->value());
//    }
//    delete iter;”
class GargantuanTable_Iterator {
    ...
};
// 如果类有人格同步前提，文档说明。如果类的实例可被多线程访问，要特别说明多线程环境相关的规则和常量使用。
```

4. 函数注释：函数声明处注释描述函数功能；定义处描述函数实现

```cpp
// 函数声明注释
// Returns true if the table cannot hold any more entries.
bool IsTableFull();

// 函数定义注释：主要说明编程技巧、实现步骤等。
```

5. 变量注释：某些情况下，需要额外的注释说明变量用途

> 每个类的数据成员都应该用注释说明用途。如果变量可以接受NULL或-1等警戒值，须加以说明

```cpp
private:
    // Keeps track of the total number of entries in the table.
    // Used to ensure we do not go over the limit. -1 means
    // that we don't yet know h
    // that we don't yet know how many entries the table has.
    int num_total_entries_;
// 全局变量也是一样
// The total number of tests cases that we run through in this regression test.
const int kNumTestCases = 6;
```

6. 实现注释：对于代码中巧妙的，晦涩的，有趣的，重要的地方加以注释

> 比较晦涩的地方要在行尾加入注释。在行尾空两格进行注释

> 不要用自然语言翻译代码作为注释。要假设读代码的人C++水平比你高，即便他可能不知道你的用意

```cpp
// If we have enough memory, mmap the data portion too.
mmap_budget = max<int64>(0, mmap_budget - index_->length());
if (mmap_budget >= data_size_ && !MmapData(mmap_chunk_bytes, mlock))
    return;  // Error already logged.
    
// 向函数传入NULL， 布尔值或整数时， 要注释说明含义，或使用常量让代码望文知意
bool success = CalculateSomething(interesting_value,
                                  10,     // Default base value.
                                  false,  // Not the first time we're calling this.
                                  NULL);  // No callback.

const int kDefaultBaseValue = 10;
const bool kFirstTimeCalling = false;
Callback *null_callback = NULL;
bool success = CalculateSomething(interesting_value,
                                  kDefaultBaseValue,
                                  kFirstTimeCalling,
                                  null_callback);
                                  
```

7. 标点，拼写和语法

> 注释的通常写法是包含正确大小写和结尾句号的完整语句. 短一点的注释 (如代码行尾注释) 可以随意点, 依然要注意风格的一致性. 完整的语句可读性更好, 也可以说明该注释是完整的, 而不是一些不成熟的想法.

> 虽然被别人指出该用分号时却用了逗号多少有些尴尬, 但清晰易读的代码还是很重要的. 正确的标点, 拼写和语法对此会有所帮助.

8. TODO 注释

> 对那些临时的, 短期的解决方案, 或已经够好但仍不完美的代码使用 TODO 注释.

```cpp

// TODO(kl@gmail.com): Use a "*" here for concatenation operator.
// TODO(Zeke) change this to use relations.

```
9. 弃用注释

> 通过弃用注释（DEPRECATED comments）以标记某接口点（interface points）已弃用.

> 您可以写上包含全大写的 DEPRECATED 的注释，以标记某接口为弃用状态。注释可以放在接口声明前，或者同一行。

> 在 DEPRECATED 一词后，留下您的名字，邮箱地址以及括号补充。

> 仅仅标记接口为 DEPRECATED     并不会让大家不约而同地弃用，您还得亲自主动修正调用点（callsites），或是找个帮手。

> 修正好的代码应该不会再涉及弃用接口点了，着实改用新接口点。如果您不知从何下手，可以找标记弃用注释的当事人一起商量。