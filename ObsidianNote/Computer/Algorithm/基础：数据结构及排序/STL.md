# string
- **字符串**是由一系列字符组成的序列。
- 在C语言中，字符串以 `'\\0'` 结尾的字符数组。
- 在C++中，常用 `std::string` 类型，功能更强大、操作更方便。

| 函数                       | 功能描述                | 示例                                                |
| ------------------------ | ------------------- | ------------------------------------------------- |
| `size()` / `length()`    | 返回字符串长度             | `int len = str.size();`                           |
| `empty()`                | 判断是否为空              | `if(str.empty())`                                 |
| `clear()`                | 清空字符串               | `str.clear();`                                    |
| `append()`               | 拼接字符串               | `str.append("abc");`                              |
| `operator+`              | 字符串拼接               | `string t = s1 + s2;`                             |
| `substr(pos, len)`       | 返回子串，从pos开始长度为len   | `string sub = s.substr(2, 3);`                    |
| `find(str, pos=0)`       | 查找子串str，返回首次出现的位置   | `int pos = s.find("abc");`                        |
| `rfind(str)`             | 查找子串最后出现的位置         | `int pos = s.rfind("abc");`                       |
| `replace(pos, len, str)` | 替换字符串               | `s.replace(0, 3, "hello");`                       |
| `insert(pos, str)`       | 插入字符串               | `s.insert(2, "xyz");`                             |
| `erase(pos, len)`        | 删除字符串               | `s.erase(2, 3);`                                  |
| `c_str()`                | 转成C字符串              | `const char* p = s.c_str();`                      |
| `to_string()`            | 数字转字符串              | `string s = to_string(123);`                      |
| `stoi()`, `stod()`       | 字符串转数字（int,double等） | `int x = stoi("123"); double d = stod("3.14");`   |
| `begin()`, `end()`       | 返回迭代器指向字符串开始和末尾     | `for(auto it = s.begin(); it != s.end(); ++it){}` |
| `at(pos)`                | 返回指定位置字符，越界抛异常      | `char c = s.at(3);`                               |
| `front()` / `back()`     | 返回首字符/尾字符           | `char c1 = s.front(); char c2 = s.back();`        |
| `compare(const string&)` | 比较两个字符串，等于0表示相等     | `int res = s1.compare(s2);`                       |
# vector
| 分类     | 函数                                    | 说明                 |
| ------ | ------------------------------------- | ------------------ |
| **构造** | `vector<T> v;`                        | 空向量                |
|        | `vector<T> v(n);`                     | 长度 `n`，默认值初始化      |
|        | `vector<T> v(n, val);`                | 长度 `n`，元素值为 `val`  |
|        | `vector<T> v2(v1);`                   | 拷贝构造               |
|        | `vector<T> v2(v1.begin(), v1.end());` | 迭代器范围构造            |
| **访问** | `v[i]`                                | 访问第 `i` 个元素（不检查越界） |
|        | `v.at(i)`                             | 访问第 `i` 个元素（检查越界）  |
|        | `v.front()`                           | 第一个元素              |
|        | `v.back()`                            | 最后一个元素             |
| **修改** | `v.push_back(x)`                      | 尾部添加元素             |
|        | `v.pop_back()`                        | 删除尾部元素             |
|        | `v.insert(pos, x)`                    | 在 `pos` 插入 `x`     |
|        | `v.erase(pos)`                        | 删除 `pos` 元素        |
|        | `v.clear()`                           | 清空                 |
|        | `v.resize(n)`                         | 改变长度               |
|        | `v.assign(n, x)`                      | 赋值为 `n` 个 `x`      |
| **容量** | `v.size()`                            | 元素个数               |
|        | `v.empty()`                           | 是否为空               |
|        | `v.capacity()`                        | 当前容量               |
|        | `v.reserve(n)`                        | 预分配容量              |
| **迭代** | `v.begin(), v.end()`                  | 正向迭代器              |
|        | `v.rbegin(), v.rend()`                | 反向迭代器              |
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    // 构造与初始化
    vector<int> v1;                   // 空向量
    vector<int> v2(5);                 // 5个0
    vector<int> v3(5, 42);             // 5个42
    vector<int> v4 = {1, 2, 3};        // 列表初始化

    // 添加与访问
    v4.push_back(4);                   // [1, 2, 3, 4]
    cout << "First: " << v4.front() << endl; // 1
    cout << "Last: " << v4.back() << endl;   // 4

    // 插入与删除
    v4.insert(v4.begin() + 1, 99);     // [1, 99, 2, 3, 4]
    v4.erase(v4.begin());              // [99, 2, 3, 4]
    v4.pop_back();                     // [99, 2, 3]

    // 遍历
    for (auto x : v4) cout << x << " "; // 99 2 3
    cout << endl;

    // 容量
    cout << "Size: " << v4.size() << ", Capacity: " << v4.capacity() << endl;

    // 清空
    v4.clear();
    cout << "Empty? " << v4.empty() << endl; // 1 (true)
}

```
# queue/priority_queue
```cpp
#include <queue>   //头文件
//queue
size()    //返回队列中元素的个数
empty()   //判空
push()    //在末尾加入一个元素
pop()     //删除第一个元素
front()/back()   //返回第一个/最后一个元素
//priority_queue
size()    //返回优先队列中元素的个数
empty()   //判空
push()    //加入一个元素
pop()     //删除堆顶元素
top()     //返回堆顶元素
默认定义为大根堆
//定义成小根堆方法：
priority_queue<int,vector<int>,greater<int>> q;

```
# stack
```cpp
#include <stack>   //头文件
size()     //返回栈元素个数
empty()    //判空
push()    //入栈
pop()    //出栈
top()    //返回栈顶元素
```
# set/multiset
```cpp
#include <set>    //头文件
//set去重,multiset不去重，均默认升序排序
//底层红黑树
size()   //返回集合中元素个数
empty()  //判空
clear()  //清空所有元素
insert()  //在集合中插入元素
erase()   //删除一个元素。
find()    //查找一个数，如果找到则返回该数第一次出现位置的迭代器，否则返回尾迭代
count()    //返回某个值元素的个数


//unordered_set
#include <unordered_set>
//底层哈希
```
# map/multimap
```cpp
#include <map>    //头文件
//map去重，multimap不去重，均默认以key值(第一属性)升序排序
//底层红黑树
size()   //返回map中元素个数
empty()  //判空
insert()  //插入元素
erase()   //删除一个元素。
find()    //同上
count()   //同上

//unordered_map
#include <unordered_map>
//底层哈希
```
# pair<int,int>
```cpp
#include <utility>    //头文件
first      //第一个元素
second     //第二个元素
//适用sort对其排序时默认以第一个元素升序排序
auto p = std::make_pair(x, y);
```
# algorithm
| 分类      | 算法函数                                 | 作用描述              | 示例代码                                                                    |
| ------- | ------------------------------------ | ----------------- | ----------------------------------------------------------------------- |
| **排序**  | `sort`, `stable_sort`                | 排序，稳定排序保持相同元素相对顺序 | `sort(v.begin(), v.end());`                                             |
| **查找**  | `find`, `binary_search`              | 查找元素，二分查找（必须有序）   | `auto it = find(v.begin(), v.end(), 3);`                                |
| **计数**  | `count`, `count_if`                  | 统计元素出现次数          | `int c = count(v.begin(), v.end(), 3);`                                 |
| **修改**  | `replace`, `replace_if`              | 替换元素              | `replace(v.begin(), v.end(), oldVal, newVal);`                          |
| **删除**  | `remove`, `remove_if`                | 删除元素（配合容器的erase）  | `v.erase(remove(v.begin(), v.end(), val), v.end());`                    |
| **复制**  | `copy`, `copy_if`                    | 复制元素              | `copy(v.begin(), v.end(), ostream_iterator<int>(cout, " "));`           |
| **变换**  | `transform`                          | 按照规则转换元素          | `transform(v.begin(), v.end(), v2.begin(), [](int x){ return x*x; });`  |
| **堆操作** | `make_heap`, `push_heap`, `pop_heap` | 堆的构造和操作           | `make_heap(v.begin(), v.end());`                                        |
| **合并**  | `merge`                              | 合并两个有序区间          | `merge(v1.begin(), v1.end(), v2.begin(), v2.end(), back_inserter(v3));` |
| **比较**  | `equal`, `lexicographical_compare`   | 比较两个区间是否相等或字典序    | `bool eq = equal(v1.begin(), v1.end(), v2.begin());`                    |
| **其它**  | `swap`, `reverse`, `rotate`          | 交换、反转、旋转元素        | `reverse(v.begin(), v.end());`                                          |
- **`sort` + `binary_search`** 是查找的黄金组合，适合大多数排序+查找需求。
- **`remove-erase` 习惯用法** 删除容器中指定元素。
- **`transform`** 做批量映射变换。
- **`reverse`、`rotate`** 是操作序列的常用利器。