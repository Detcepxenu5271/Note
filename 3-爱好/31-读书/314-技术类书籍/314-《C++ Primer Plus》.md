# 《C++ Primer Plus》
第 6 版 (中文版)

## 临时笔记
第 4 章: new, delete
第 8 章: 函数模板
第 9+ 章

## 章节笔记
### 第 4 章 复合类型
#### 4.2 字符串
\#getline
cin 读取一行 C 数组型字符串
* `cin.getline(str, size[, delim])`
	- size 包括 '\0'
	- 读取换行符并丢弃, 不保存到字符串中
* `cin.get(str, size[, delim])`
	- 类似 getline, 也默认读到换行停止
	- 不读取换行符, 换行符留在输入队列
	- 读入多行数据时, 可使用重载 `cin.get()` 读取单个字符 (换行符)
	- 可以连用, 如 `cin.get(...).get(...)`, 因为 get 返回 cin 对象

#### 4.3 string 类简介
string 可以用 `cin >> str` 等 I/O, 但不能用 `cin.getline(str, size)`, 应该用 `getline(cin, str)`

字符串字面值
* `L"This is a sentence"`: w_char
* `u"This is a sentence"`: char_16
* `U"This is a sentence"`: char_32
* (以下是 C++11 新增)
* `u8"This is a sentence"`: UTF-8
* `R"(This is a sentence)"`: 原始 (raw)
	- 注意界定符是 `"(` 和`)"`
	- 界定符的引号和括号间可以插入任意相同的若干字符, 如果字符串中需要出现原界定符的话就需要这么做

#### 4.4 结构简介
位域
* 在结构中指定字段的 bits 长度, 可以省空间
* 结构所占空间为变量长度的倍数 (如定义 unsigned int, 则结构长度为 4B, 8B, ...)
* (自测) 以 unsigned int 4B 为例, 在同一段 4B 内, 字段的位分配可以跨字节; 在不同段 4B, 字段的位分配不能跨越, 如果前一段 4B 分配不下, 就要从下一段开始分配

```c
#include <stdio.h>

// XXllllll lkkkjjjj | Xiiiiihh hhgggggg fffffeee ddddccba
typedef struct Bits {
	// 0 - 7
	unsigned int a : 1; // 0
	unsigned int b : 1; // 1
	unsigned int c : 2; // 2-3
	unsigned int d : 4; // 4-7
	// 8 - 15
	unsigned int e : 3; // 8-10
	unsigned int f : 5; // 11-15
	// 16 - 25 (23+2)
	unsigned int g : 6; // 16-21
	unsigned int h : 4; // 22-25
	// 26 - 30
	unsigned int i : 5; // 26-30

	// next 4B
	unsigned int j : 4; // 32-35
	unsigned int k : 3; // 36-38
	unsigned int l : 7; // 39-45
} Bits;

void printBits(Bits bits) {
	int size = sizeof(bits);
	unsigned char *p = (unsigned char *)&bits;

	int i, j;
	for (i = size - 1; i >= 0; i--) {
		unsigned char data = *(p + i);
		for (j = 7; j >= 0; j--) {
			putchar( '0' + ((data>>j)&1) );
		}
		if (i) putchar(' ');
	}
	putchar('\n');
}

int main() {
	Bits bits;
	// XX100000 11011001 | X1000100 00111111 00000111 00001101
	bits.a = 1;
	bits.b = 0;
	bits.c = 3;
	bits.d = 0;
	bits.e = 7;
	bits.f = 0;
	bits.g = 63;
	bits.h = 0;
	bits.i = 17;
	bits.j = 9;
	bits.k = 5;
	bits.l = 65;
	printBits(bits);

	return 0;
}
```

#### 4.5 共用体
匿名共用体: 在 struct 中使用匿名共用体, 共用体成员名也是 struct 中的成员名 (不能同时使用这些成员), 不需要中间标识符
```c
struct widget {
	char brand[20];
	int type;
	// 不匿名, 要用 xxx.id_val.id_num
	union id {long id_num; char id_char[20];} id_val;
	// 匿名, 只要用 xxx.id_num
	union {long id_num; char id_char[20];};
}
```

#### 4.6 枚举
枚举可以设置相同的值, 例如把 null 和 zero 枚举量都指定为 0

枚举在 C++ 中有取值范围. 另外, 所占空间也不固定

#### 4.7 指针和自由存储空间
? 指针与 C++ 基本原理
* OOP 强调运行阶段决策 (动态分配空间)
* 过程性编程强调编译阶段决策 (静态分配空间)

new 分配数组时, 长度信息是不公用的 (delete[] 知道, 用户不知道), 需要自己跟踪

#### 4.8 指针、数组和指针算数
数组名被解释为第一个元素的地址, 数组名的地址被解释为数组的地址. 两者值相同, 但表示的内存块大小不同
```c
short tell[10];

//  tell == &tell

//  tell + 1: + 2B
// &tell + 1: +20B

// 定义指向 tell 第一个元素的指针
short *p1 = tell;
short *p2 = &tell[0];

// 定义指向 tell 数组的指针
short (*pa)[10] = &tell; // 注: short *ap[10] 表示指针数组
```

内存泄露问题: 可以通过 C++ 中的智能指针缓解

#### 4.9 类型组合
auto 类型推断

#### 4.10 数组的替代品
array: 类似数组, 长度固定 (定义时长度必须是常量), 可以通过 `.at()` 成员函数检查越界

### 5 循环和关系表达式
### 16 string 类和标准模板库
#### 16.1 string 类
\#find

string 的查找
* `text.find(pattern[, pos, n])` 在 text 中查找 pattern 的前 n 个字符组成的字符串, 找到则返回首次出现的位置, 否则返回 `string::npos`
* `text.find(ch[, pos])` 在 text 中查找字符 ch 首次出现的位置...
* `rfind`, `find_first_of`, `find_last_of`, `find_first_not_of`, `find_last_not_of`

string 的内存申请
* 申请一段比需要稍大的内存, 不够时重新申请更大的
* 一般的实现中, 内存按 `n * 16 - 1` 分配
* `str.capacity()` 查看当前的容量大小
* `reserve(n)` 调整 capacity 大于等于 n
* `resize(n[, ch])` 调整 size 为 n (有效数据区域), 比原来短则截断, 比原来长则用 ch 填充

#### 16.2 智能指针模板类
\#智能指针

**!!!注意 智能指针只应该用于堆内存 (如 new 申请的内存), 不能用于非堆内存**

`auto_ptr` 不建议使用
`unique_ptr` 一个指针对应一个对象, 赋值会使所有权转让
    - 可以用 `new` 或 `new[]` 分配内存, 后者例子: `std::unique_ptr<double[]> pda (new double(5))`
    - 使用 `std::move()` 转让所有权
`share_ptr` 多个指针对应一个对象, 赋值会让对象的智能指针计数 +1
    - 只可以用 `new` 分配内存
        + 一个回答说 C++11 不行, C++17 行, 但是我测试都行(?

`unique_ptr` 可以作为右值赋给 `share_ptr`, 而 `share_ptr` 会接管原来归 `unique_ptr` 所有的对象

#### 16.3 标准模板库
迭代器
* 广义指针, 支持解引用 (`operator*()`) 和递增 (`operator++()`) 操作, 可以让 STL 对无法使用简单指针的类也提供统一接口
* 定义, 例如: `vector<double>::iterator pd;` (不想写复杂的类型, 也可以使用 auto)

常用方法
* `size()`
* `swap(a, b)`
* `begin()` 和 `end()`
    - `end()` 指向最后一个元素的下一个元素, 具体实现各异, 不应该解引用
    - Q: 为什么 `end()` 不指向最后一个元素?
        A: 指向下一个, 能使得一般规则覆盖边界条件. 例如对于空数组和非空数组, "指向下一个" 可以同样地用 "begin == end" 判断, 而 "指向最后一个" 需要特殊处理 end
* `push_back(elem)`
* `erase(iter1, iter2)`
* `insert()`
    - 对 vector: `v.insert(pos, iter1, iter2)` 在 v 的 pos 处(前)插入 `[iter1, iter2)` 的元素


