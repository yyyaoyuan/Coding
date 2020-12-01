# 两数之和

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那两个整数，并返回他们的数组下标。
你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

# 解法一：暴力搜索

# 解法二：哈希查找

对于每一个 x，我们首先查询哈希表中是否存在 target - x，然后将 x 插入到哈希表中，即可保证不会让 x 和自己匹配。

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        if not nums:
            return 
        hashtable = {}
        for i in range(len(nums)):
            if target-nums[i] in hashtable:
                return [hashtable[target-nums[i]], i]
            hashtable[nums[i]] = i
```

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        if not nums:
            return 
        hashtable = {}
        for i, val in enumerate(nums):           # 注意学习这种写法
            if target-val in hashtable:
                return [hashtable[target-val], i]
            hashtable[val] = i
```

# 感想

今天吃饭和师兄聊到了这一题，然后顺便做一下，学习一下，没有想到哈希表还可以这样来用，真的很神奇！！！

需要学习的知识点—枚举：
```python
for i, val in enumerate(nums):
```
