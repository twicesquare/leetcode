# 一、算术运算符
```
# 1. 基本运算
a, b = 10, 3

print(a + b)   # 13  加法
print(a - b)   # 7   减法
print(a * b)   # 30  乘法
print(a / b)   # 3.3333333333333335  除法（返回浮点数）
print(a // b)  # 3   整除（向下取整）
print(a % b)   # 1   取模（求余数）
print(a ** b)  # 1000  幂运算（10的3次方）

# 2. 正负号
print(+a)      # 10  正号
print(-a)      # -10 负号
```

# 二、比较（关系）运算符
```
a, b = 10, 3

print(a == b)   # False  等于
print(a != b)   # True   不等于
print(a > b)    # True   大于
print(a < b)    # False  小于
print(a >= b)   # True   大于等于
print(a <= b)   # False  小于等于

# 链式比较
x = 5
print(1 < x < 10)      # True
print(1 < x and x < 10) # 等价写法
```

# 三、逻辑运算符
```
a, b = True, False

print(a and b)   # False  与（两个都为真才为真）
print(a or b)    # True   或（至少一个为真）
print(not a)     # False  非（取反）

# 短路运算
def test():
    print("执行了")
    return True

print(False and test())  # False，test()不会执行
print(True or test())    # True，test()不会执行

# 实际应用
user_input = ""
result = user_input or "默认值"  # "默认值"
```

# 四、位运算符
```
a, b = 5, 3  # 二进制: a=0101, b=0011

print(a & b)   # 1   按位与 (0101 & 0011 = 0001)
print(a | b)   # 7   按位或 (0101 | 0011 = 0111)
print(a ^ b)   # 6   按位异或 (0101 ^ 0011 = 0110)
print(~a)      # -6  按位取反 (～0101 = 1010，补码表示)
print(a << 1)  # 10  左移 (0101 << 1 = 1010)
print(a >> 1)  # 2   右移 (0101 >> 1 = 0010)

# 位运算应用
# 判断奇偶
print(5 & 1)   # 1（奇数）
print(4 & 1)   # 0（偶数）

# 乘以2的幂
print(5 << 3)  # 40 (5 * 8)

# 除以2的幂
print(16 >> 2) # 4 (16 / 4)
```

# 五、赋值运算符
```
x = 10
print(x)   # 10  基本赋值

x += 5     # x = x + 5
print(x)   # 15

x -= 3     # x = x - 3
print(x)   # 12

x *= 2     # x = x * 2
print(x)   # 24

x /= 4     # x = x / 4
print(x)   # 6.0

x //= 2    # x = x // 2
print(x)   # 3.0

x %= 2     # x = x % 2
print(x)   # 1.0

x **= 3    # x = x ** 3
print(x)   # 1.0

# 位运算赋值
x = 5
x &= 3     # x = x & 3
print(x)   # 1

x |= 2     # x = x | 2
print(x)   # 3

x ^= 1     # x = x ^ 1
print(x)   # 2

x <<= 1    # x = x << 1
print(x)   # 4

x >>= 1    # x = x >> 1
print(x)   # 2
```

# 六、身份运算符
```
a = [1, 2, 3]
b = [1, 2, 3]
c = a

print(a is c)     # True   同一对象
print(a is b)     # False  不同对象
print(a is not b) # True   不是同一对象

# 与 == 的区别
print(a == b)     # True   值相等
print(a is b)     # False  不是同一对象

# 常见用法
if x is None:
    print("x是None")
```

# 七、成员运算符
```
lst = [1, 2, 3, 4, 5]

print(3 in lst)      # True   存在
print(6 in lst)      # False  不存在
print(3 not in lst)  # False  不存在（取反）

# 字符串应用
text = "Hello World"
print("Hello" in text)    # True
print("Hi" not in text)   # True

# 字典应用
d = {'a': 1, 'b': 2}
print('a' in d)       # True（检查键）
print(1 in d.values()) # True（检查值）
```

# 八、运算符优先级
```
# 从高到低排序
# 1. 括号 ()
# 2. 幂运算 **
# 3. 正负号 +x, -x
# 4. 乘法 *, 除法 /, 整除 //, 取模 %
# 5. 加法 +, 减法 -
# 6. 移位 <<, >>
# 7. 位与 &
# 8. 位异或 ^
# 9. 位或 |
# 10. 比较 <, >, <=, >=, !=, ==
# 11. 身份 is, is not
# 12. 成员 in, not in
# 13. 逻辑非 not
# 14. 逻辑与 and
# 15. 逻辑或 or

# 示例
result = 2 + 3 * 4 ** 2
# 先算 4**2=16
# 再算 3*16=48
# 最后 2+48=50
print(result)  # 50

# 使用括号改变优先级
result = (2 + 3) * 4 ** 2
# 先算 (2+3)=5
# 再算 4**2=16
# 最后 5*16=80
print(result)  # 80
```

# 九、特殊运算符
## 1. 海象运算符（Python 3.8+）
```
# := 可以在表达式中赋值
if (n := len([1, 2, 3])) > 2:
    print(f"长度为{n}")  # 长度为3

# 循环中使用
while (line := input()) != "quit":
    print(f"输入: {line}")

# 列表推导式
[n for i in range(3) if (n := i * 2) > 2]  # [4]
```

## 2. 条件运算符（三元运算符）
```
# value_if_true if condition else value_if_false
age = 18
status = "成年" if age >= 18 else "未成年"
print(status)  # 成年

# 嵌套使用
score = 85
grade = "A" if score >= 90 else "B" if score >= 80 else "C"
print(grade)  # B
```

# 十、矩阵运算（NumPy）
```
import numpy as np

a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

# 矩阵乘法
print(a @ b)           # 32 (1*4 + 2*5 + 3*6)

# 矩阵点积
print(np.dot(a, b))    # 32

# 矩阵运算
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

print(A @ B)  # 矩阵乘法
```

# 十一、运算符重载示例
```
class Vector:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)
    
    def __str__(self):
        return f"Vector({self.x}, {self.y})"

v1 = Vector(1, 2)
v2 = Vector(3, 4)
print(v1 + v2)  # Vector(4, 6)
```
