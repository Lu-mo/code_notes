# lintcode 31 数组划分 中等
[31.数组划分](https://www.lintcode.com/problem/partition-array/description)

## 正解思路:双指针交换+二分查找
```
class Solution:
    """
    @param nums: The integer array you should partition
    @param k: An integer
    @return: The index after partition
    """
    def partitionArray(self, nums, k):
        # write your code here
        n = len(nums)
        if n < 1:
            return 0
            
        l = 0
        r = n - 1 
        while l<r:
            if nums[l]<k and nums[r]>=k:
                l += 1 
                r -= 1 
            elif nums[l]<k:
                l += 1 
            elif nums[r]>=k:
                r -= 1 
            else:
                nums[l],nums[r] = nums[r],nums[l]
                l += 1 
                r -= 1 
        #print(nums)
        
        l = 0
        r = n - 1
        while l + 1 < r:
            mid = (l+r) // 2
            if nums[mid] >= k:
                r = mid
            else:
                l = mid
        
        if nums[l] < k:
            return r if r != n-1 or (nums[r]>=k) else n
        else:
            return l
```           


## 精简版正解:换完其实不用二分
```
class Solution:
    """
    @param nums: The integer array you should partition
    @param k: An integer
    @return: The index after partition
    """
    def partitionArray(self, nums, k):
        # write your code here
        n = len(nums)
        if n < 1:
            return 0
            
        l = 0
        r = n - 1 
        while l<r:
            if nums[l]<k and nums[r]>=k:
                l += 1 
                r -= 1 
            elif nums[l]<k:
                l += 1 
            elif nums[r]>=k:
                r -= 1 
            else:
                nums[l],nums[r] = nums[r],nums[l]
                l += 1 
                r -= 1 
        #print(l)
        
        if nums[l]>=k:
            return l
        else:
            if l == 0:
                return 0
            elif l == n-1:
                return n 
            else:
                return l+1
```


## 偷鸡思路:与求数组中最大/最小K个数思路一致,不用排序数组,计数即可


### answer 1
```
class Solution:
    """
    @param nums: The integer array you should partition
    @param k: An integer
    @return: The index after partition
    """
    def partitionArray(self, nums, k):
        # write your code here
        n = len(nums)
        #if n<1:
        #    return 0
        
        count = 0
        for i in range(n):
            if nums[i]<k:
                count += 1
                
        return count
```

### answer 2
```
class Solution:
    """
    @param nums: The integer array you should partition
    @param k: An integer
    @return: The index after partition
    """
    def partitionArray(self, nums, k):
        # write your code here
        return len([x for x in nums if x < k])
```
