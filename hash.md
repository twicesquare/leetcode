# lc中hash相关题目

## 205 同构字符串
### 双哈希表解法
```
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        if len(s) != len(t):
            return False

        s_to_t = {}
        t_to_s = {}

        for char_s, char_t in zip(s, t):
            if char_s in s_to_t:
                if s_to_t[char_s] != char_t:
                    return False
            else:
                s_to_t[char_s] = char_t

            if char_t in t_to_s:
                if t_to_s[char_t] != char_s:
                    return False
            else:
                t_to_s[char_t] = char_s

        return True
```

### 比较两个字符串中每个字符第一次出现的索引序列
```
def isIsomorphic(s: str, t: str) -> bool:
    # 比如 s = "paper", t = "title"
    # s 的索引序列：[0, 1, 0, 3, 4] (p在0位, a在1位, p又是0位...)
    # t 的索引序列：[0, 1, 0, 3, 4] (t在0位, i在1位, t又是0位...)
    # 如果两个序列相同，则同构
    return list(map(s.find, s)) == list(map(t.find, t))
```

**`s.find`：寻找“第一次”**

`s.find(sub)` 是字符串的一个内置方法。它的功能是：返回子字符串 `sub` 在 `s` 中第一次出现的索引（下标）。

**`map(s.find, s)`：批量处理**

`map(function, iterable)` 会把 `function` 作用到 `iterable` 的每一个元素上。

在这里，s 是一个字符串（可以看作字符列表），`map` 会遍历 s 中的每一个字符，并对它执行 `s.find`。

**`list(...)`：将结果具象化**

map 在 Python 3 中返回的是一个“迭代器”（Iterator），它很懒，不会立刻生成所有数据。为了能进行比较，我们需要用 list() 强行把这些结果变成一个真正的列表。

`list(map(s.find, "paper"))` 得到 [0, 1, 0, 3, 4]

`list(map(t.find, "title"))` 得到 [0, 1, 0, 3, 4]
