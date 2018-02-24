Search in Rotated Sorted Array II
=====

1.问题描述
-----

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.<br>
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).<br>
Write a function to determine if a given target is in the array.<br>
The array may contain duplicates.<br>
假设按升序排列的数组在预先未知的某个关键点处进行旋转。（即，0 1 2 4 5 6 7可能变成4 5 6 7 0 1 2）。编写一个函数来确定给定的目标是否在数组中。该数组可能包含重复项。<br>


2.思路
----

把给定的数与数组中的数依次比较即可。<br>

3.代码
---

```c
bool search(int* nums, int numsSize, int target) {
    int temp=0;
    for (int i=0; i<numsSize; i++) {
        if (target==nums[i]) {
            temp=1;
            break;
        }
    }
    return temp==1;
}
```

4.总结
----

在return temp==1;中，一开始写的是return temp=1;造成错误，判断语句要有==来判断相等，=号是赋值的符号。
