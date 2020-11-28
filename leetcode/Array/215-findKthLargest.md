# 数组中的第K个最大元素

在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

## 示例 1:

输入: [3,2,1,5,6,4] 和 k = 2

输出: 5

# 解答：递归+分治

按照快速排序的思想进行解决，

* 首先需要一个pivot，记录一下，然后将其弹出
* 接着将数组按照是否大于该值进行划分，numsL，numsR
* 然后进行判断：
  * if len(numsR) == k-1: return pivot
  * if len(numsR) > k-1: 对numsR进行递归
  * if len(numsL) < k-1: 对numsL进行递归，但是此时需要求出新的k值：k = k - 1- len(numsR)

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        pivot = nums[0]
        nums.pop(0)      # 这里弹出是未了防止每次选取的pivot相同，如果len(numsR) > k的话，就会出现刚才的问题，所以需要弹出
        numsL = [i for i in nums if i < pivot]    # 这个代码牢记
        numsR = [i for i in nums if i >= pivot]

        if len(numsR) == k - 1:               # 递归终止条件
             return pivot
        elif len(numsR) > k - 1:
             return self.findKthLargest(numsR, k)   # 这个比较好理解
        else:
             k = k - 1 - len(numsR)                  # 这里需要酸楚新的k，因为已经弹出了一个数字，所以k也变成了k-1，然后减去比较大的部分数组的长度
             return self.findKthLargest(numsL, k)
```

# 感想：

旷世科技面试遇到了这道题，当时面试官一直在说有没有更快的方法，我当时想了一下说，难道可以O(n)时间解决？？？面试官最后给了提示，快排的思想，不过自己并没有写出来，当时陷入了二分之中。
还是需要好好努力！！！加油！！！！！！
