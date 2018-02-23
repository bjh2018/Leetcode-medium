Find the Duplicate Number
===

1.问题描述
----

Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.<br> 
Note:<br>
You must not modify the array (assume the array is read only).<br>
You must use only constant, O(1) extra space.<br>
Your runtime complexity should be less than O(n2).<br>
There is only one duplicate number in the array, but it could be repeated more than once.<br>
给定的一长度为n+1的数组，数组里的数在1和n之间，则数组中至少有一个数重复，假设只有一个数重复，输出这个数。<br>
注意：<br>
不得修改数组（假定数组只读）。<br>
必须只使用恒定的O（1）额外空间。<br>
运行时复杂度应该小于O（n^2）。<br>
数组中只有一个重复数字，但可以重复多次。<br>

2.思路
----

把数组遍历，找出重复的数字即可。<br>

3.代码
---

```c
int findDuplicate(int* nums, int numsSize) {
    int result=0;
    for(int i=0; i<numsSize; i++) {
        for (int j=0; j<numsSize; j++) {
            if (nums[i]==nums[j]&&i!=j) {
                result=nums[i];
                break;
            }
        }
    }
    return result;
}
```
