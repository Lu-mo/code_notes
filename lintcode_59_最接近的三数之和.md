# lintcode 59 最接近的三数之和 中等
[最接近的三数之和](https://www.lintcode.com/problem/3sum-closest/description)
## 思路和三数之和一致,排序,取一个,双指针求另外两个

```
class Solution:
    """
    @param numbers: Give an array numbers of n integer
    @param target: An integer
    @return: return the sum of the three integers, the sum closest target.
    """
    def threeSumClosest(self, numbers, target):
        # write your code here
        def closer(x,y,target):
            return x if abs(x-target)<abs(y-target) else y
            
        n = len(numbers)
        if n<=2:
            return None 
        if n == 3:
            return sum(numbers)
        
        numbers.sort()
        
        temp_sum = sum(numbers[:3])
        for i in range(n-2):
            t = target - numbers[i]
            l = i + 1 
            r = n - 1
            
            while l < r:
                temp = numbers[l] + numbers[r]
                if temp == t:
                    return target
                elif temp < t:
                    l += 1
                    temp_sum = closer(temp_sum,temp+numbers[i],target)
                else:
                    r -= 1
                    temp_sum = closer(temp_sum,temp+numbers[i],target)
        
        return temp_sum    
```
