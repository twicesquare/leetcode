# 基本数据类型
Python 是**动态类型语言**，不需要声明类型。

| 类型 | 示例 | 特点 |
| :--- | :--- | :--- |
| int / float | a = 10, b = 3.14 | 数字运算 |
| str | s = "Hello" | 字符串，支持切片 |
| bool | is_ready = True | 首字母必须大写 |
| NoneType | x = None | 表示空值 |

# 容器类型
Python 的灵魂，复习重点在于它们的**括号和特性**。

## `List` (列表) `[]`

列表是可变的（Mutable），支持索引和切片。

增: `append(x)` (末尾添加), `insert(index, x)` (指定位置插入), `extend(list2)` (合并列表)。

删: `pop(index)` (删除并返回指定位置元素，默认最后), `remove(value)` (删除第一个匹配的值), `clear()` (清空)。

查/改: `list[0] = "new"` (修改), `list.index(x)` (查找索引), `list.count(x)` (统计次数)。

排: `sort()` (原地排序), `reverse()` (原地反转)。

## `Tuple` (元组) ()

有序、不可变。

一旦创建就不能修改。常用于函数返回多个值或作为字典的键。

操作: 仅支持 `count()` 和 `index()`。

**注意: 只有一个元素的元组必须加逗号：`t = (1,)`。**

## `Dict` (字典) `{key: value}`
无序（Python 3.7+ 保持插入顺序）、键值对。高效的键值映射

增/改: `d["key"] = value` (若键存在则修改，不存在则新增), `update(d2)` (批量更新)。

删: `del d["key"]`, `pop("key")` (返回被删的值), `popitem()` (删除最后一对)。

查: `d["key"]` (不存在会报错), `d.get("key", default)` (推荐：不存在返回默认值)。

遍历: `d.keys()`, `d.values()`, `d.items()` (获取键值对)。

## `Set` (集合) `{}`
无序、元素唯一。常用于去重。

操作: `add(x)`, `remove(x)`, `discard(x)` (删除不存在的元素不报错)。

数学运算: & (交集), | (并集), - (差集)。

## `deque`
双端队列

`list` 的局限：list.pop(0) 的时间复杂度是 O(n)。因为删掉第一个元素后，后面所有的元素都要往挪一位。如果列表有 100 万个元素，这会非常慢。

`deque` 的优势：`deque.popleft()` 的时间复杂度是 O(1)。它是为了频繁的左右两端增删而设计的。

| 操作 | 代码 | 说明 |
| :--- | :--- | :--- |
| 创建 | `dq = deque([1, 2])` | 可以从列表初始化 |
| 右侧入队 | `dq.append(x)` | 在末尾添加 |
| 左侧入队 | `dq.appendleft(x)` | 在开头添加 |
| 右侧出队 | `val = dq.pop()` | 删除并返回末尾元素 |
| 左侧出队 | `val = dq.popleft()` | BFS 核心：删除并返回开头元素 |
| 查看大小 | `len(dq)` | 获取当前元素个数 |
| 旋转 | `dq.rotate(1)` | 将末尾元素移到开头 |

# `heap`

大顶堆 (Max Heap)：任意节点的值都大于其子节点的值。堆顶（根节点）是整个堆中的最大值。

小顶堆 (Min Heap)：任意节点的值都小于其子节点的值。堆顶（根节点）是整个堆中的最小值。

注意：Python 的内置模块 `heapq` 默认实现的全部是 **小顶堆**。

如果需要实现大顶堆，就把所有值`*-1`

使用堆之前，需要先 `import heapq`。它直接操作原有的列表。

| 函数 | 功能 | 时间复杂度 |
| :--- | :--- | :--- |
| `heapify(list)` | 将列表原地转换为堆 | $O(n)$ |
| `heappush(heap, item)` | 向堆中加入一个元素，并保持堆特性 | $O(\log n)$ |
| `heappop(heap)` | 弹出并返回堆顶（最小）元素 | $O(\log n)$ |
| `nlargest(k, iterable)` | 返回最大的 K 个元素 | $O(n \log k)$ |
| `nsmallest(k, iterable)` | 返回最小的 K 个元素 | $O(n \log k)$ |

## 普通list VS 堆化后的list

虽然转换前后的 nums 看起来都只是一个 `[]` 包围的列表，但它们内部元素的排列逻辑完全变了。

普通 list：元素按照你放入的顺序排列，没有任何逻辑联系。

堆化后的 list：元素被重新排列，满足**父节点永远小于子节点**的完全二叉树结构。

如果不执行 `heapify`，直接对一个普通列表使用 `heappop` 或 `heappush`，堆的规则就会失效。

## heap取最大的n个数

**nlargest(k, iterable)：取最大的 $k$ 个数**

**独立性：它并不依赖你传入的 `nums` 是否已经是一个堆。无论 `nums` 是乱序的、排序好的、还是已经堆化过的，`nlargest` 都能准确找到结果。**

这个函数会返回 `iterable` 中最大的 $k$ 个元素，并按 **降序（从大到小）** 排列。

底层逻辑：它先取输入数据的前 $k$ 个元素，建立一个小顶堆（注意：找最大的数反而用小顶堆）。

遍历剩余的 $n-k$ 个元素。如果新元素比堆顶（当前 $k$ 个数里的最小值）大，就剔除堆顶，把新元素挤进去。

遍历结束时，堆里剩下的就是最大的 $k$ 个。

```
import heapq

nums = [1, 8, 2, 23, 7, -4, 18, 23, 42, 37, 2]
result = heapq.nlargest(3, nums)
print(result)  # 输出: [42, 37, 23]
```
## heap取最小的n个数

**nsmallest(k, iterable)：取最小的 $k$ 个数**

同理，它返回最小的 $k$ 个元素，并按 **升序（从小到大）** 排列。

底层逻辑：它内部会维护一个大顶堆（找最小的数反而用大顶堆），确保堆顶永远是当前“潜力最小候选组”里最大的那个，一旦发现更小的就替换它。

## heap代码示例
```
import heapq

nums = [3, 1, 4, 1, 5, 9, 2]
heapq.heapify(nums)  # 把列表变成堆：[1, 1, 2, 3, 5, 9, 4]

# 弹出最小值
print(heapq.heappop(nums))  # 输出 1

# 添加新值
heapq.heappush(nums, 0)
print(nums[0])  # 堆顶现在是 0

# 堆顶永远是这 k 个数里最小的
heapq.nlargest(k, nums)[-1]
```

# 切片操作 (Slicing)

切片适用于字符串、列表和元组，语法为 `[start:stop:step]`。

```
nums = [0, 1, 2, 3, 4, 5]
print(nums[1:4])   # [1, 2, 3] (左闭右开)
print(nums[::-1])  # [5, 4, 3, 2, 1, 0] (快速反转)
print(nums[::2])   # [0, 2, 4] (步长为2)
```

# 控制流
Python 使用**缩进**来定义代码块。

## 条件判断if
```
if score >= 90:
    print("A")
elif score >= 60:
    print("Pass")
else:
    print("Fail")
```

## 循环
`for i in range(5)`: (循环 0 到 4)。

`for item in my_list`: (直接遍历元素)。

`while condition`: (满足条件时循环)。

## break 与 continue
`break`: 彻底终结整个循环（不论循环还没跑完多少轮）。

`continue`: 跳过当前这一轮剩余的代码，直接进入下一轮。

```
# 示例：只打印 10 以内的偶数，但遇到 8 就停止
for i in range(10):
    if i % 2 != 0:
        continue  # 是奇数就跳过，不执行 print
    if i == 8:
        break     # 到了 8 就彻底退出
    print(i)      # 输出: 0, 2, 4, 6
```

## 带索引的遍历：enumerate
如果你需要在循环时既知道“内容”又知道“位置（第几个）”

```names = ["Alice", "Bob", "Charlie"]
for index, name in enumerate(names):
    if index == 1:
        print(f"找到第二个人了: {name}")
```

# 列表推导式 (List Comprehension)
压缩代码长度

```
# 语法：[表达式 for 变量 in 可迭代对象 if 条件]
squares = [x**2 for x in range(10) if x % 2 == 0]
# 结果: [0, 4, 16, 36, 64]
```

# 函数与异常处理
## 定义函数`def`
```
def greet(name="Guest"):
    return f"Hello, {name}!"
```

## 错误捕获
```
try:
    res = 10 / 0
except ZeroDivisionError:
    print("不能除以零")
finally:
    print("无论如何都会执行")
```

`finally` 块里的代码无论是否发生错误，都一定会执行。

即便 `try` 成功了，它会执行。

即便 `try` 失败被 `except` 捕获了，它也会执行。

用途：通常用于“清理现场”，比如关闭已经打开的文件、关闭数据库连接等。

### 异常类型

`ZeroDivisionError`是 `Python` 预定义的异常类型。`Python`知道在数学中不能除以 0。当你尝试 `10 / 0` 时，Python 会抛出一个名为 `ZeroDivisionError` 的错误。

如果你不写 `except ZeroDivisionError`，程序就会直接崩溃（显示红色的报错信息）。

如果你写了，就相当于告诉 Python：“如果发生‘除零错误’，按我写的代码办（比如打印一句提示），别让程序挂掉。”

**常见异常类型还有：**

`ValueError`: 传入的值类型对，但值不对（比如 int("abc")）。

`TypeError`: 类型不对（比如 1 + "2"）。

`IndexError`: 索引超出了列表范围。

# 内置函数
| 分类 | 函数 | 用途 |
| :--- | :--- | :--- |
| 类型转换 | `int()`, `str()`, `list()`, `dict()`, `set()`, `float()` | 数据类型互转 |
| 数学运算 | `abs(x)`, `max(a, b, ...)`, `min()`, `sum([1, 2, 3])`, `round()`, `pow()` | 绝对值、最值、求和、四舍五入 |
| 序列处理 | `len(s)`, `sorted(list)`, `reversed()`, `enumerate(list)`, `zip(list1, list2)`, `range(start, stop)` | 长度、排序(原列表不变)、反转、带索引遍历、打包、生成数字序列 |
| 输入输出 | `print()`, `input()` | 打印、接收键盘输入 |
| 判断/检查 | `type(x)`, `isinstance()`, `help()`, `dir()` | 查看类型、检查对象、查看帮助文档 |
| 逻辑 | `all()`, `any()` | 检查列表里是否全部为真 / 是否有任一为真 |
