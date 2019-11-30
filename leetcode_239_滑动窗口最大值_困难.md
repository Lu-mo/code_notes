# leetcode 239 滑动窗口最大值 困难
[滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/)

## 双向队列
    需要维护一个递减序列保证最大值滑出窗口后有值接替,并且跳过不会是区间最大值的数字
    队首为最大值O(1)
    时间复杂度O(n)
```
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        from collections import deque
        n = len(nums)
        lens = 0
        if n < 1:
            return None
        queue = deque()
        result = []
        for i in range(n):
            #if len(queue) == 0:
            #    queue.append(i)
            #    continue
            while lens>0 and nums[i] > nums[queue[-1]]:
                queue.pop()
                lens -= 1
            queue.append(i)
            lens += 1
            if i >= k-1:
                while lens>0 and queue[0] <= i-k:
                    queue.popleft()
                    lens -= 1
                result.append(nums[queue[0]])
        
        return result
```
