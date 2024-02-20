---
layout:     post   				    
title:      代码随想录算法训练营第一天|LeetCode704 二分查找、LeetCode27 移除元素
subtitle:   
date:       2024-2-20				
author:     慕念 						
header-img: img/coding.jpg
catalog: true 						
tags:								
    - Coding
---

# LeetCode704 二分查找

> 题目链接：https://leetcode.cn/problems/binary-search/
>
> 文章讲解：[https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html](https://programmercarl.com/0704.二分查找.html)
>
> 视频讲解：https://www.bilibili.com/video/BV1fA4y1o715

一开始直接暴力遍历求解：

```python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """

        for i in range(len(nums)):
            if nums[i] == target:
                return i
        return -1
```

后来想起题目是二分查找，看了视频教程之后再改了一下：

## 左闭右闭区间

```python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left = 0
        right = len(nums) - 1

        while left <= right: 	# 左闭右闭区间[1,1]
            mid = (left + right) // 2
            if nums[mid] > target:
                right = mid - 1 
            elif nums[mid] < target:
                left = mid + 1
            else:
                return mid
        return -1
```

## 左闭右开区间

```python
class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left = 0
        right = len(nums) # 注意取值

        while left < right: # 左闭右开区间[1,1)
            mid = (left + right) // 2
            if nums[mid] > target:
                right = mid 
            elif nums[mid] < target:
                left = mid + 1
            else:
                return mid
        return -1
```



> 相关题目：35.搜索插入位置 和 34. 在排序数组中查找元素的第一个和最后一个位置 



# LeetCode27 移除元素

> 题目链接：https://leetcode.cn/problems/remove-element/ 
>
> 文章讲解：[https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html](https://programmercarl.com/0027.移除元素.html)
>
> 视频讲解：https://www.bilibili.com/video/BV12A4y1Z7LP 

暴力遍历，python用remove删除数组元素：

```python
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """

        while 1:
            if val in nums:
                nums.remove(val)
            else:
                return len(nums)
```

> Python list列表删除元素（4种方法）https://blog.csdn.net/yelitoudu/article/details/117952380

## 双指针法

⭐快指针寻找新数组里需要的元素（即删除目标值后的元素）

⭐新数组需要更新的下标是慢指针，把快指针的值赋给慢指针

![img](https://munian-1308672375.cos.ap-shanghai.myqcloud.com/images/202402210107565.gif)

⭐如果fast对应值不等于val，是新数组需要的元素，需要对nums[slow]进行替换

```python
class Solution(object):
    def removeElement(self, nums, val):
        """
        :type nums: List[int]
        :type val: int
        :rtype: int
        """

        slow = 0
        fast = 0

        while fast < len(nums):
            if nums[fast] != val:
                # slow 用来收集不等于 val 的值，如果 fast 对应值不等于 val，则把它与 slow 替换
                nums[slow] = nums[fast] 
                slow += 1
            fast += 1 
        return slow    # 正好是新数组的大小
```

