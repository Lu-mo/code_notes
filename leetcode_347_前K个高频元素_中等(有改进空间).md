# leetcode 347 前K个高频元素 中等
[前K个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/submissions/)
## 用heapq构建最小堆,构建类型用字典值做比较函数参数
    知识点一:Python3取消了__cmp__函数,改为(__lt__, __le__, __gt__, or __ge__)等方法,
            结合以下代码段实现用两个方法自动推导出其他方法
            ```
            from functools import total_ordering
            @total_ordering
            ```
    知识点二:Python3优先队列源码由heapq构成

```
class Solution:
    from functools import total_ordering
    @total_ordering
    class ComparableObj:
        def __init__(self, k, v):
            self.v = v
            self.k = k
            
        def __cmp__(self, other):
            if self.v < other.v:
                return -1
            elif self.v == other.v:
                return 0
            else:
                return 1
        
        def __eq__(self,other):
            return self.v == other.v
        
        def __lt__(self,other):
            return self.v < other.v

    def topKFrequent(self, nums: List[int], n: int) -> List[int]:
        import heapq
        dic = dict(collections.Counter(nums))
        #print(dic)
        pqueue = []

        count = 0
        for k,v in dic.items():
            if count == n:
                heapq.heappushpop(pqueue,Solution.ComparableObj(k,v))
                continue
            count += 1
            #print(k,v)
            #print(count==n)
            heapq.heappush(pqueue,Solution.ComparableObj(k,v))
        #print(pqueue)
        
        
        count = 0
        list = []
        while count<n:
            obj = heapq.heappop(pqueue)
            list.append(obj.k)
            count += 1

        list.reverse()
        return list
```
