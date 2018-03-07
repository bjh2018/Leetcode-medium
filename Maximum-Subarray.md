Maximum Subarray
===

1.问题描述
---

Find the contiguous subarray within an array (containing at least one number) which has the largest sum. <br>
For example, given the array [-2,1,-3,4,-1,2,1,-5,4],<br>
the contiguous subarray [4,-1,2,1] has the largest sum = 6. <br>
给定一个数组，求连续的子数组中个元素相加的和的最大值。

2.思路
---

这个题目和上次做的那个求连续的的子数组中元素的乘积的最大值类似，所一改变子数组的开头可以通过首尾分别相加来实现，在加法中结果最小就是结果为负数，而要使结果最大，
就可以在当其中有一边的和是负数的时候，就改变它的开头，从下一个元素开始重新加。

3.代码
---

```c
int max(int x, int y) {
    if (x>y) return x;
    else return y;
}
int maxSubArray(int* nums, int numsSize) {
    int left=0,right=0;
    int sum=-2147483647;
    for (int i=0; i<numsSize; i++) {
        left=left+nums[i];
        right=right+nums[numsSize-i-1];
        sum=max(sum,max(left,right));
        left=left<0?0:left;
        right=right<0?0:right;
    }
    return sum;
}
```

4.总结
---

正反向分别相加或者相乘就可以只取其中最大的就行，因为相反方向的运行会改变当前方向没有改变的子数组的开头。
