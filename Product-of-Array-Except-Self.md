Product of Array Except Self
====

1.问题描述
----

Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].<br>
Solve it without division and in O(n).<br>
For example, given [1,2,3,4], return [24,12,8,6].<br>
给定一个数组，把每个元素都换成除了它本身其他数的乘积。

2.思路
---

如果要是直接一个一个来写的话，就很容易超时，但是可以先从左边开始把指定元素左边的全都乘上，在建立一个循环把右边的元素乘上，就可以减少很多时间。<br>

3.代码
---

```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* productExceptSelf(int* nums, int numsSize, int* returnSize) {
    int *res=(int *)malloc(sizeof(int)*numsSize);
        res[0]=1;
    for (int i=1; i<numsSize; i++) {
        res[i]=nums[i-1]*res[i-1];
    }
    int temp=1;
    for (int i=numsSize-2; i>=0; i--) {
        temp=temp*nums[i+1];//因为nums[i]与nums[i+1]在之前已经进行过其他操作，不再满足res[i]=res[i+1]*nums[i+1]，所以用一个temp来缓冲
        res[i]=res[i]*temp;
    }
    *returnSize=numsSize;
    return res;
}
```

4.总结
---

要注意从左边和从右边乘以指定的数时，情况不同，要分情况讨论。<br>
