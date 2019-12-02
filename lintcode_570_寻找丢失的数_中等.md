# lintcode_570_寻找丢失的数_中等
[lintcode_570_寻找丢失的数_中等](https://www.lintcode.com/problem/find-the-missing-number-ii/description)

## 严重失误,太睿智了,题目输入给出了序列可能包含的最大值,跑去自己算了.
###  难点一:最后获得的序列列表可能少了多个值(无效分割),这种情况需排除
## 优化
```
            if n == 0:
                if len(result) == limit - 1:
                    return sums - sum(result)
                else:
                    return None
```

```
class Solution:
    """
    @param n: An integer
    @param str: a string with number from 1-n in random order and miss one number
    @return: An integer
    """
    def findMissing2(self, n, str):
        # write your code here
        global sums
        global lens,limit
        def DFS(s,result):
            global limit
            n = len(s)
            if n == 0:
                #print(result)
                t = []
                for i in range(1,limit+1):
                    if i not in result:
                        t.append(i)
                #print("t",t)
                if len(t) == 1:
                    return t[0]
                else:
                    return None
            else:
                if s[0] != "0":
                    if int(s[:2]) not in result and int(s[:2]) <= limit:
                        r1 = DFS(s[2:],result+[int(s[0:2])]) 
                        if r1 != None:
                            return r1
                    if int(s[:1]) not in result and int(s[:1]) <= limit:
                        r1 = DFS(s[1:],result+[int(s[0:1])])
                        if r1 != None:
                            return r1
                    return None
                else:
                    return None
        
        
        lens = len(str)
        
        #if lens <= 9:
        #    limit = 10
        #else:
        #    temp = (lens - 9) % 2
        #    if temp == 1:
                # 缺1位数字
        #        limit = (lens-8)//2 + 9 + 1
        #    else:
        #        limit = (lens - 9)//2 + 9 + 1
        limit = n
        #print(limit)
        return DFS(str,[])
```
