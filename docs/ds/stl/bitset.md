## 介绍

 `std :: bitset` 是标准库中的一个**固定大小**序列，其储存的数据只包含 `0/1` 

众所周知，由于内存地址是按字节即 `byte` 寻址，而非比特 `bit` ,

我们一个 `bool` 类型的变量，虽然只能表示 `0/1` , 但是也占了 `1byte` 的内存

 `bitset` 就是通过固定的优化，使得一个字节的八个比特能分别储存 8 位的 `0/1` 

对于一个 4 字节的 `int` 变量，在只存 `0/1` 的意义下， `bitset` 占用空间只是其 $\frac{1}{32}$ 

在某些情况下通过 `bitset` 可以使你的复杂度除以 32

当然， `vector` 的一个特化 `vector<bool>` 的储存方式同 `bitset` 一样，区别在于其支持动态开空间，

 `bitset` 则和我们一般的静态数组一样，是在编译时就开好了的。

那么为什么要用 `bitset` 而非 `vector<bool>` ?

通过以下的介绍，你可以更加详细的看到 `bitset` 具备的方便操作

```cpp
#include <bitset>  // 包含 bitset 的头文件
```

### 运算符

-    `operator[]` : 访问其特定的一位

-    `operator ==/！=` : 比较两个 `bitset` 内容是否完全一样

-    `operator &=/|=/^=/~` : 进行按位与/或/异或/取反操作
-    `operator <</>>/<<=/>>=` : 进行二进制左移/右移
-    `operator <</>>` : 流运算符，这意味着你可以通过 `cin/cout` 进行输入输出

     `vector<bool>` 只具有前两项

### 成员函数

-    `test()` : 它和 `vector` 中的 `at()` 的作用是一样的，和 `[]` 运算符的区别就是越界检查
-    `count()` : 返回 `true` 的数量
-    `set()` : 将整个 `bitset` 设置成 `true` , 你也可以传入参数使其设置成你的参数
-    `reset()` : 将整个 `bitset` 设置成 `false` 
-    `flip()` : 翻转该位 (0 变 1,1 变 0), 相当于逻辑非/异或 1
-    `to_string()` : 返回转换成的字符串表达
-    `to_ulong()` : 返回转换成的 `unsigned long` 表达 ( `long` 在 NT 及 32 位 POSIX 系统下与 `int` 一样，在 64 位 POSIX 下与 `long long` 一样）
-    `to_ullong()` **C++11**, 返回转换成的 `unsigned long long` 表达

这些 `vector<bool>` 基本都没有

## 作用

一般来讲，我们可以用 `bitset` 优化一些可行性 DP, 或者线筛素数 ( `notprime` 这种 `bool` 数组可以用 `bitset` 开到 $10^8$ 之类的）

它最主要的作用还是压掉了内存带来的时间优化， $\frac{1}{32}$ 的常数优化已经可以是复杂度级别的优化了，比如一个 $N = 1000$ 的 $O(N^3)$ 算法， $10^9$ 显然很卡，在常数大一点的情况下必然卡不过去，**O（松）不能算！**, 这时候如果我们某一维除以 32, 则可以比较保险的过了这道题

其实 `bitset` 不光是一个容器，更是一种思想，我们可以通过手写的方式，来把 `long long` 什么的压成每 bit 表示一个信息，用 STL 的原因更多是因为它的运算符方便
