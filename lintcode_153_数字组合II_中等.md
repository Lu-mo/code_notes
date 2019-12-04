# lintcode_153_数字组合II_中等
[lintcode_153_数字组合II_中等](https://www.lintcode.com/problem/combination-sum-ii/description)


###      1.题目明明写着数字之和,单个数字也可以真的服了
###      2.数组指针设置失误没有达到最后一个数字
###      3.终止条件失误没有设置对
###      4.不知道能不能优化
###      5.得解超时

```
class Solution:
    """
    @param num: Given the candidate numbers
    @param target: Given the target number
    @return: All the combinations that sum to target
    """
    def combinationSum2(self, num, target):
        # write your code here
        global nums,results
        def DFS(index,target,result):
            #print(index,target,result)
            global nums,results
            if 0 == target:
                #result.append(nums[index])
                #if len(result) == 1:
                #    return False
                #else:
                if result not in results:
                    results.append(result)
                return True
            else:
                while index < len(nums) and target >= nums[index]:
                    #result.append(nums[index])
                    if DFS(index+1,target-nums[index],result+[nums[index]]) == True:
                        break
                    index += 1
                return         
        n = len(num)
        results = []
        if n < 1:
            return results
        
        num.sort()
        nums = num
        DFS(0,target,[])
        return results
            
```
