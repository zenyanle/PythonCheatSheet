# Python 速查表

一份📜可以用来在**更短时间内复习** Python 语法的速查表。特别适合用来**解决数据结构与算法问题**，或在面试前快速过一遍。

# 目录

- [基础](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
- [数据结构](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
    - [列表（Lists）](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
    - [字典（Dictionary）](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
    - [计数器（Counter）](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
    - [双端队列（Deque）](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
    - [堆（Heapq）](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
    - [集合（Sets）](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
    - [元组（Tuples）](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
    - [字符串（Strings）](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
- [内置函数](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
- [进阶主题](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
- [最佳实践](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)
- [小技巧与易错点](https://www.notion.so/CheatSheet-1e37e2a5d82e802992bed72493fa68cb?pvs=21)

# 基础

## 数据类型

![](https://user-images.githubusercontent.com/59110866/173563442-1a6fa3d2-b569-4eb0-99cc-9b91cc8be1eb.png)

## 运算符优先级

![](https://user-images.githubusercontent.com/47276307/172329850-61fc0809-a4b0-416c-848b-1c502ecb4772.jpg)

# 数据结构

## 列表（Lists）

时间复杂度参考：

![](https://user-images.githubusercontent.com/47276307/172330098-1c5f0a6e-7f80-4f4f-9be6-1d734e2c70cd.jpg)

```python
nums = [1,2,3]

# 常用操作
nums.index(1)      # 查找元素位置
nums.append(1)     # 末尾添加元素
nums.insert(0,10)  # 指定位置插入（在开头插入10）
nums.remove(3)     # 移除指定元素
nums.pop()         # 移除并返回最后一个元素
nums.sort()        # 原地排序（TimSort: O(n log n)）
nums.reverse()     # 原地反转
nums.copy()        # 浅拷贝列表

# 切片操作
nums[start:stop:step]  # 通用切片语法
nums[-1]    # 最后一个元素
nums[::-1]  # 反转列表
nums[1:]    # 从索引1开始到结尾
nums[:3]    # 前三个元素

```

## 字典（Dictionary）

时间复杂度参考：

![](https://user-images.githubusercontent.com/47276307/172330107-e68e3228-1c76-4bfb-bb38-04d18f94d5b9.jpg)

```python
d = {'a':1, 'b':2}

# 基本操作
d.get('key', default)     # 安全访问，有默认值
d.setdefault('key', 0)    # 若不存在则设置默认值
d.items()                 # 获取键值对
d.keys()                  # 获取所有键
d.values()                # 获取所有值
d.pop(key)                # 删除并返回指定键的值
d.update({key: value})    # 批量更新键值对

# 进阶用法
from collections import defaultdict
d = defaultdict(list)     # 自动初始化缺失的键
d = defaultdict(int)      # 常用于计数

```

## 计数器（Counter）

```python
from collections import Counter

# 初始化
c = Counter(['a','a','b'])    # 通过可迭代对象
c = Counter("hello")          # 通过字符串

# 常用操作
c.most_common(2)      # 返回出现次数最多的两个元素
c['a'] += 1           # 增加计数
c.update("more")      # 批量增加计数
c.total()             # 所有计数的总和

```

## 双端队列（Deque）

时间复杂度参考：

![](https://user-images.githubusercontent.com/47276307/172330115-78500420-3276-4e45-8ce3-fd668b7eb14e.jpg)

```python
from collections import deque

# 适合 BFS —— 两端 O(1) 操作
d = deque()
d.append(1)          # 右侧添加元素
d.appendleft(2)      # 左侧添加元素
d.pop()              # 移除右侧元素
d.popleft()          # 移除左侧元素
d.extend([1,2,3])    # 批量添加到右侧
d.extendleft([1,2,3])# 批量添加到左侧（顺序反转）
d.rotate(n)          # 向右旋转n步（负数向左）

```

## 堆（Heapq）

```python
import heapq

# 最小堆（MinHeap）操作 - 除 heapify 外都是 O(log n)
nums = [3,1,4,1,5]
heapq.heapify(nums)          # 原地堆化 O(n)
heapq.heappush(nums, 2)      # 添加元素 O(log n)
smallest = heapq.heappop(nums)  # 弹出最小元素 O(log n)

# 最大堆技巧：元素取相反数
nums = [-x for x in nums]
heapq.heapify(nums)
largest = -heapq.heappop(nums)

# 进阶操作
k_largest = heapq.nlargest(k, nums)    # O(n * log k)
k_smallest = heapq.nsmallest(k, nums)  # O(n * log k)

# 自定义优先队列
heap = []
heapq.heappush(heap, (priority, item))  # 按优先级排序

```

## 集合（Sets）

时间复杂度参考：

![](https://user-images.githubusercontent.com/47276307/172330132-7a785f5f-bbc6-43b9-b82f-794190813787.jpg)

```python
s = {1,2,3}

# 常用操作
s.add(4)             # 添加元素
s.remove(4)          # 移除元素（不存在则抛错）
s.discard(4)         # 移除元素（不存在不抛错）
s.pop()              # 移除并返回任意元素

# 集合运算
a.union(b)           # 并集
a.intersection(b)    # 交集
a.difference(b)      # 差集
a.symmetric_difference(b)  # 对称差集
a.issubset(b)        # 子集判断
a.issuperset(b)      # 超集判断

```

## 元组（Tuples）

```python
# 元组是不可变列表
t = (1, 2, 3, 1)

# 基本操作
t.count(1)      # 统计某元素出现次数
t.index(2)      # 查找元素索引

# 常用模式
x, y = (1, 2)   # 元组解包
coords = [(1,2), (3,4)]  # 用元组组成列表

```

## 字符串（Strings）

```python
s = "hello world"

# 常用方法
s.split()            # 按空格分割
s.split(',')         # 按逗号分割
s.strip()            # 去除首尾空白
s.lower()            # 转为小写
s.upper()            # 转为大写
s.isalnum()          # 检查是否是字母数字
s.isalpha()          # 检查是否是纯字母
s.isdigit()          # 检查是否全是数字
s.find('sub')        # 查找子串索引（找不到返回-1）
s.count('sub')       # 子串出现次数
s.replace('old', 'new')  # 替换子串

# ASCII 转换
ord('a')             # 字符转ASCII（97）
chr(97)              # ASCII转字符（'a'）

# 拼接列表
''.join(['a','b'])   # 连接成字符串

```

# 内置函数

```python
# 迭代辅助
enumerate(lst)        # 获取索引和值
zip(lst1, lst2)       # 并行迭代
map(fn, lst)          # 应用函数
filter(fn, lst)       # 筛选
any(lst)              # 任一为 True 返回 True
all(lst)              # 全部为 True 返回 True

# 二分查找（需要 import bisect）
bisect.bisect(lst, x)      # 查找插入位置
bisect.bisect_left(lst, x) # 查找最左插入位置
bisect.insort(lst, x)      # 插入并保持有序

# 类型转换
int('42')            # 字符串转整数
str(42)              # 整数转字符串
list('abc')          # 字符串转列表
''.join(['a','b'])   # 列表转字符串
set([1,2,2])         # 列表转集合

# 数学相关
abs(-5)              # 绝对值
pow(2, 3)            # 幂
round(3.14159, 2)    # 四舍五入到小数点后2位

```

# 进阶内容

## 使用 cmp_to_key 进行自定义排序

```python
from functools import cmp_to_key

def compare(item1, item2):
    # 返回 -1 表示 item1 排在前
    # 返回 1 表示 item2 排在前
    # 返回 0 表示相等
    if item1 < item2:
        return -1
    elif item1 > item2:
        return 1
    return 0

# 使用自定义比较函数排序
sorted_list = sorted(items, key=cmp_to_key(compare))

```

## 多输入处理

```python
# 基本多输入
x, y = input("输入两个值：").split()

# 多个整数输入
x, y = map(int, input("输入两个数字：").split())

# 一组整数列表输入
nums = list(map(int, input("输入一组数字：").split()))

# 自定义分隔符的输入
values = input("输入逗号分隔的值：").split(',')

# 列表推导式版本
x, y = [int(x) for x in input("输入两个数字：").split()]

```

## math 模块常用方法

```python
import math

# 常量
math.pi       # 圆周率 3.141592653589793
math.e        # 自然对数底 2.718281828459045

# 常见函数
math.ceil(2.3)        # 向上取整，返回 3
math.floor(2.3)       # 向下取整，返回 2
math.gcd(a, b)        # 最大公约数
math.log(x, base)     # 以 base 为底的对数
math.sqrt(x)          # 平方根
math.pow(x, y)        # x 的 y 次方（整数优先使用 **）

# 三角函数
math.degrees(rad)     # 弧度转角度
math.radians(deg)     # 角度转弧度

```

## Python 中重要的整数运算

```python
# 二进制表示
bin(10)              # '0b1010'
format(10, 'b')      # '1010'（不带 '0b' 前缀）

# 除法与取余
divmod(10, 3)        # (3, 1)，返回 (商, 余数)

# 负数处理
x = -3
y = 2
print(x // y)        # -2（地板除，向下取整）
print(int(x/y))      # -1（通常更符合期望）
print(x % y)         # 1（Python 负数取模特性）

```

# 最佳实践

## 注释与文档

```python
def binary_search(arr, target):
    """
    使用二分查找在有序数组中寻找目标值。
    参数:
        arr: 已排序的数字列表
        target: 要查找的目标值
    返回:
        目标值的索引，找不到则返回 -1
    """
    pass

```

## 测试

```python
# 使用断言处理边界测试
assert binary_search([], 1) == -1, "空数组应返回 -1"
assert binary_search([1], 1) == 0, "单元素数组应正确返回"

```

# 技巧与坑点

1. 整数除法：

```python
# 用 int() 保证负数处理一致
print(-3//2)        # 返回 -2
print(int(-3/2))    # 返回 -1（通常更合理）

```

1. 默认字典：

```python
# 频率统计推荐用 defaultdict
from collections import defaultdict
freq = defaultdict(int)
for x in lst:
    freq[x] += 1    # 避免 KeyError

```

1. 堆优先级处理：

```python
# 自定义优先级使用元组
heap = []
heapq.heappush(heap, (priority, item))

```

1. 列表推导式：

```python
# 比 map/filter 更清晰
squares = [x*x for x in range(10) if x % 2 == 0]

```

1. 字符串构建：

```python
# 构建字符串推荐用 join()
chars = ['a', 'b', 'c']
word = ''.join(chars)  # 更高效

```

1. 使用集合提高效率：

```python
# O(1) 时间复杂度进行元素查找
seen = set()
if x in seen:  # 比列表查找快得多
    print("找到了！")

```

1. 自定义排序键：

```python
# 先按长度再按字典序排序
words.sort(key=lambda x: (len(x), x))

```

1. 默认参数警告：

```python
# 避免可变默认值导致的 bug
def bad(lst=[]):     # 可能产生意外共享
    lst.append(1)
    return lst

def good(lst=None):  # 推荐写法
    if lst is None:
        lst = []
    lst.append(1)
    return lst

```
