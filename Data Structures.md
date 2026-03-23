# 快速排序
```
import random

class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        # 我们要找的是第 k 大，转换成索引就是：
        # 升序排序后的第 len(nums) - k 个
        target = len(nums) - k
        
        def quick_select(left, right):
            # 随机选择枢轴，防止最坏情况
            pivot_idx = random.randint(left, right)
            pivot = nums[pivot_idx]
            
            # 将枢轴交换到最后
            nums[pivot_idx], nums[right] = nums[right], nums[pivot_idx]
            
            # 分区操作：小于 pivot 的放左边
            i = left
            for j in range(left, right):
                if nums[j] <= pivot:
                    nums[i], nums[j] = nums[j], nums[i]
                    i += 1
            nums[i], nums[right] = nums[right], nums[i]
            
            # 判断当前枢轴的位置 i
            if i == target:
                return nums[i]
            elif i < target:
                return quick_select(i + 1, right)
            else:
                return quick_select(left, i - 1)
                
        return quick_select(0, len(nums) - 1)
```
