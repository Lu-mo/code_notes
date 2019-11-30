# leetcode 739 每日温度 中等
[每日温度](https://leetcode-cn.com/problems/daily-temperatures/submissions/)
## 用栈保存递减序列,出现会破坏序列的就弹出,时间复杂度O(n),避免了重复搜索

```
class Solution:
    def dailyTemperatures(self, T: List[int]) -> List[int]:
        stack = []
        n = len(T)
        if not n:
            return []
        result = [0]*n
        for i in range(n):
            if stack == []:
                stack.append(i)
                continue
            if T[stack[-1]] >= T[i]:
                stack.append(i)
                continue
            #count = 0
            while stack != [] and T[stack[-1]] < T[i]:
                #count += 1
                index = stack.pop()
                result[index] = i-index#count
            stack.append(i)
        return result
```
