# lintcode 5 第k大元素 中等
[第k大的数](https://www.lintcode.com/problem/kth-largest-element/description)
## 非挑战解 15.00%

```
class Solution:
    """
    @param n: An integer
    @param nums: An array
    @return: the Kth largest element
    """
    def kthLargestElement(self, n, nums):
        # write your code here
        import heapq
        lens = len(nums)
        if lens<1:
            return None
        
        return heapq.nlargest(n,nums)[n-1]
```

## 挑战解 
### answer1 部分分治排序,超过1.00%,效率太低

```
class Solution:
    """
    @param n: An integer
    @param nums: An array
    @return: the Kth largest element
    """
    def kthLargestElement(self, n, nums):
        # write your code here
        def partition(nums,start,end,n):
            print(start,end)
            if start + 1 >= end:
                return nums[n]
            pivot = nums[(start+end)//2]
            left, right = start, end 
            while left < right:
                while left < right and nums[left]>pivot:
                    left += 1 
                while left < right and nums[right]<pivot:
                    right -= 1 
                if left < right:
                    nums[left],nums[right] = nums[right],nums[left]
                    left += 1 
                    right -= 1
            print(nums)
            if n <= left:
                return partition(nums,start,left,n)
            elif n >= right:
                return partition(nums,right,end,n)
            else:
                return nums[n]
                
        lens = len(nums)
        if lens<1:
            return None
        
        return partition(nums,0,lens-1,n-1)
  ```
