# lintcode_652_分割回文串_中等
[lintcode_652_分割回文串_中等](https://www.lintcode.com/problem/palindrome-partitioning/description)

## 20分钟内写完,判断回文串还可以再优化

```
class Solution:
    """
    @param: s: A string
    @return: A list of lists of string
    """
    def partition(self, s):
        # write your code here
        global results
        global setTrue,setFalse
        setTrue,setFalse = set(),set()
        results = []
        
        def DFS(s,result):
            global results
            lens = len(s)
            if lens == 0:
                results.append(result)
                return
            else:
                right = lens - 1 
                while 0<=right:
                    if isPalin(right,s):
                        DFS(s[right+1:],result+[s[:right+1]])
                    right -= 1
                return
        
        def isPalin(right,s):
            global setTrue,setFalse
            tstr = s[:right+1]
            if  tstr in setTrue:
                return True 
                
            elif tstr in setFalse:
                return False
                
            else:
                l = 0
                r = right
                while l<=r:
                    if tstr[l] != tstr[r]:
                        break
                    l += 1 
                    r -= 1 
                if l>r:
                    setTrue.add(tstr)
                    return True
                else:
                    setFalse.add(tstr)
                    return False
        
        DFS(s,[])
        return results
```
