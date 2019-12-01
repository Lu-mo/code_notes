# leetcode_785_判断二分图_中等(可优化)
[判断二分图](https://leetcode-cn.com/problems/is-graph-bipartite/)

## 首先思考两个节点集合或者BFS,但是受边出现顺序会导致误判,只能DFS
```diff
-bfs可行
```
###   要点: 二分图判断就用着色+深度,矛盾就确定不是二分图
###   疑点: 如果有孤岛是不是随便丢尽任意集合?

```
class Solution:
    def isBipartite(self, graph: List[List[int]]) -> bool:
        global color
        def DFS(node):
            global color
            stack = graph[node]
            while stack:
                node2 = stack.pop()
                if color[node2] == -color[node]:
                    continue
                elif color[node2] == 0:
                    color[node2] = -color[node]
                    result = DFS(node2)
                    if result == False:
                        return False
                else:
                    return False
            return True


        n = len(graph)

        color = [0] * n
        i = 0
        while i < n:
            if color[i] == 0:
                color[i] = 1
                if DFS(i) == False:
                    return False
            i += 1
        return True
```
