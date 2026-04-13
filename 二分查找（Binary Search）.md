# 二分查找
## 前提
目标数组必须是有序的（通常是升序）。

## 核心逻辑：排除法
二分查找通过不断比较“中间值”与“目标值”，每次都能将搜索范围缩小一半。

设定指针：定义两个指针 left 和 right，分别指向数组的开头和结尾。

计算中间索引：找到中间位置 mid。

比较并缩小范围：

如果 `nums[mid] == target`：找到了，直接返回索引。

如果 `nums[mid] < target`：说明目标在右半边，将 left 移到 mid + 1。

如果 `nums[mid] > target`：说明目标在左半边，将 right 移到 mid - 1。

循环：重复上述过程，直到 left > right（没找到）。

## 标准代码模板
```
def binarySearch(nums: list, target: int) -> int:
    left = 0
    right = len(nums) - 1 # 闭区间 [left, right]
    
    while left <= right:
        # 防止溢出的写法（虽然 Python 会自动处理大数，但在 C++/Java 中很重要）
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1  # 目标在右侧，左边界右移
        else:
            right = mid - 1 # 目标在左侧，右边界左移
            
    return -1 # 未找到
```
