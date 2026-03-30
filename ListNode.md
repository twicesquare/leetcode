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
