# lintcode_426_恢复IP地址_中等
[lintcode_426_恢复IP地址_中等](https://www.lintcode.com/problem/restore-ip-addresses/description)

## easy

```
class Solution:
    """
    @param s: the IP string
    @return: All possible valid IP addresses
    """
    def restoreIpAddresses(self, s):
        # write your code here
        global results
        def DFS(s,result):
            global results
            if s == "" and result.count(".") == 4:
                results.append(result.rstrip("."))
            else:
                n = len(s)
                if result.count(".")>3:
                    return 
                if n >= 1 and int(s[0])>=0:
                    DFS(s[1:],result+s[0]+".")
                if n >= 2 and int(s[:2]) >= 10 and int(s[:2]) <100:
                    DFS(s[2:],result+s[0:2]+".")
                if n >= 3 and int(s[:3]) >= 100 and int(s[:3]) <256:
                    DFS(s[3:],result+s[0:3]+".")
                return
        
        n = len(s)
        results = []
        if n < 4 or n > 12:
            return results
            
        DFS(s,"")
        return results
```
