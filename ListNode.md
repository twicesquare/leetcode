# 基础操作

# 快慢指针

# 翻转列表
## 例题，H100.25
```
class Solution:
    def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        # 翻转一个小链表的辅助函数
        def reverse(head: ListNode):
            pre = None
            curr = head
            while curr:
                nxt = curr.next
                curr.next = pre
                pre = curr
                curr = nxt
            return pre

        dummy = ListNode(0, head)
        pre = dummy

        while True:
            # 1. 找到当前组的结尾 end
            end = pre
            for i in range(k):
                end = end.next
                if not end: # 如果不够 k 个，直接返回结果
                    return dummy.next
            
            # 2. 记录下一组的开始，并断开当前组
            start = pre.next
            next_group = end.next
            end.next = None
            
            # 3. 翻转当前组，并接回到主链表
            pre.next = reverse(start)
            
            # 4. 把翻转后的尾部（即原来的 start）连上后面
            start.next = next_group
            
            # 5. 指针接力：pre 移动到下一组的前驱位置
            pre = start

        return dummy.next
```

# 深拷贝（含random）
## 关于哈希表和字典
哈希表（Hash Table）是“原理”，而字典（Dictionary）是 Python 里的“实现”

哈希表是一种存储数据的数据结构，它最大的特点是：快。它通过一个“哈希函数”，把你的 键（Key） 转化成一个 索引（Index），直接定位到内存里的某个位置。

不用找：在普通链表里找东西，你要从头摸到尾；在哈希表里，你给它 Key，它直接告诉你地址。时间复杂度：理想情况下是 $O(1)$，也就是无论里面有一百个节点还是一个亿，速度都一样。

## 字典（Dict）是怎么用哈希表的？

在 Python 中，当你写 `mapping[curr] = Node(curr.val)` 时，后台发生了这些事：

取哈希值：Python 调用 `hash(curr)`。因为 `curr` 是一个对象，它的内存地址就是它的唯一标识。

映射索引：把哈希值通过计算，变成字典内部大数组的一个下标。

存放值：在这个下标的位置，存入你的新节点 Node(curr.val)。

## HOT100 138
执行 `mapping[curr] = Node(curr.val)` 后，字典内部存储的是：

`{ 0x111 : 0x888 }`

**字典里面的键值对实际上值不一定要是值，也可以是别的形式，比如node**，字典的“值（Value）”可以是任何对象

键 (Key)：必须是不可变的（比如数字、字符串、或者对象的唯一身份标识），这样才能通过它快速计算出存放位置。
```
# 字典的值可以是各种各样的形式：
mapping = {
    "age": 25,                          # 值是整数 (int)
    "name": "Gemini",                   # 值是字符串 (str)
    "scores": [90, 80, 70],             # 值是列表 (list)
    "info": {"city": "Shanghai"},       # 值是另一个字典 (dict)
    "curr_node": Node(10),              # 值是一个 Node 对象 (Object)
}
```

题目解法
```
"""
"""
# Definition for a Node.
class Node:
    def __init__(self, x: int, next: 'Node' = None, random: 'Node' = None):
        self.val = int(x)
        self.next = next
        self.random = random
"""

class Solution:
    def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        if not head: return None

        # 使用字典映射，先存储旧键新值，val存在，指针另外再看
        curr = head
        mapping = {} #先空字典
        while curr:
            mapping[curr] = Node(curr.val)
            curr = curr.next
        
        # 建立地址的映射
        curr = head # 返回头节点处
        while curr:
            if curr.next: #就是如果有指向就执行，没有就置空
                mapping[curr].next = mapping[curr.next] 
                # 比如 mapping[0x001] = Node(7) Node(7)实际是新分配了一个地址为0x008
                # mapping[0x001].next实际上是0x008.next
                # 然后等于mapping[0x002(0x001.next的地址空间)]
                # 而在上一步创建时mapping[0x002] = Node(13),即为0x009的地址
                # 所以能够创建 0x008.next = 0x009, 对应原来的0x001.next = 0x002
            if curr.random:
                mapping[curr].random = mapping[curr.random]
            
            curr = curr.next
        
        return mapping[head] # 即mapping[0x001] = 0x008开始的空间
```
