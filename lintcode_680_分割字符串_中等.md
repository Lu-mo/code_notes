# lintcode_680_分割字符串_中等
[680_分割字符串_中等](https://www.lintcode.com/problem/split-string/description)

## 列出所有情况,简单的递归深度优先遍历,全局变量保存结果

```
class Solution:
    """
    @param: : a string to be split
    @return: all possible split string array
    """

    def splitString(self, s):
        # write your code here
        global results
        results = []
        def DFS(s,result):
            global results
            lens = len(s)
            if lens == 0:
                results.append(result)
                return ""
            elif lens == 1:
                results.append(result+[s])
                return s
            else:
                DFS(s[1:],result+[s[:1]])
                DFS(s[2:],result+[s[:2]])
                return s
        
        DFS(s,[])
        return results
```
