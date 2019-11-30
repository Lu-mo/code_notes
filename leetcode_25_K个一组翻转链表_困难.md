# leetcode 25 K个一组翻转链表 困难
[K个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)
## 取出k个为一组进行翻转,之后与原链表重新连接，不算递归空间复杂度O(1),时间复杂度O(n)+O(n),战胜88.48%
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        def reverse(pre,node,end,end_next):
            if end == node:
                node.next = pre
                return node
            else:
                new_head = reverse(node,node.next,end,end_next)
                node.next = pre
                return new_head

        root = ListNode(-1)
        root.next = head 
        node = head
        pre = root 
        while node:
            counter = 1
            while node and counter<k:
                #print(node.val)
                node = node.next
                counter += 1
            if node == None:
                return root.next
            elif counter == k:
                plast = node.next
                new_end = pre.next
                new_head = reverse(pre,pre.next,node,node.next)
                pre.next = new_head
                new_end.next = plast
                node = plast
            pre = new_end
            #print(pre.val)
        return root.next
```
