# 插入排序

从第二个元素开始，依次将其和前面的元素进行对比，如果小于前面的元素便交换位置，直至遍历完所有元素。

```python
def insert_sort(data):
    for i in range(1, len(data)):
        for j in range(i, 0, -1):
            if data[j] < data[j-1]:
                data[j], data[j-1] = data[j-1], data[j]
    return data
```

# 感想

插入排序和冒泡排序有些类似，核心代码中都有相邻元素的比较，主要的不同在于：
* 插入排序是利用当前元素作为基准，然后使其和前面所有的元素一一比较，然后插入到合适的位置。
* 冒泡排序是相邻元素比较，没有基准值。

加油，开始慢慢有些感觉了，多多练习，你一定够可以的，加油！！！