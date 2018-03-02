Find Minimum in Rotated Sorted Array
=====

1.问题描述
----

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.<br>
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).<br>
Find the minimum element.<br>
You may assume no duplicate exists in the array.<br>
已经排好序的数组在某个特定的位置发生反转，找出改变后的数组中最小的数。

2.思路
---

我觉得与其找到转折点，去找最小值，不如简单粗暴地直接找最小值。

3.代码
----

```c
int findMin(int* nums, int numsSize) {
    int min=2147483647;
    for (int i=0; i<numsSize; i++) {
        if (nums[i]<min) {
            min=nums[i];
        }
    }
    return min;
}
```


