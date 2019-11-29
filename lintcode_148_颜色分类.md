# lintcode 148 颜色分类 中等
[148.颜色分类](https://www.lintcode.com/problem/sort-colors/description)
## 正解 三指针
index指针只有三种情况 0/1/2

```
class Solution:
    """
    @param nums: A list of integer which is 0, 1 or 2 
    @return: nothing
    """
    def sortColors(self, nums):
        # write your code here
        n = len(nums)
        left = 0
        index = 0
        right = n - 1
        
        while index <= right:
            if nums[index] == 0:
                nums[left],nums[index] = nums[index],nums[left]
                index += 1 
                left += 1
            elif nums[index] == 2:
                nums[right],nums[index] = nums[index],nums[right]
                #index += 1 
                right -= 1
            else:
                index += 1
            
        return nums
  ```
  
