Single Number III
===

1.问题描述
---

Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.<br> 
For example: <br>
Given nums = [1, 2, 1, 3, 2, 5], return [3, 5]. <br>
Note:<br>
The order of the result is not important. So in the above example, [5, 3] is also correct.<br>
给定的数组中只有特殊元素只出现一次，其他元素都出现两次，找出特殊的元素并返回。

2.代码I
---

```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* singleNumber(int* nums, int numsSize, int* returnSize) {
    int *ans=(int *)malloc(sizeof(int )*numsSize);
    int temp=0, size=0;
    for (int i=0; i<numsSize; i++) {
        for (int j=0; j<numsSize; j++) {
            if (nums[i]==nums[j]) {
                temp++;
            }
        }
        if (temp==1) {
            ans[size++]=nums[i];
        }
        temp=0;
    }
    *returnSize=size;
    return ans;
}
```

3.代码II
---

```c
int* singleNumber(int* nums, int numsSize, int* returnSize) {
    int *ans=(int *)malloc(sizeof(int )*2);
    ans[0]=0;
    ans[1]=0;
    int diff=0;
    for (int i=0; i<numsSize; i++) {
        diff^=nums[i];
    }
    diff&=-diff;
    for (int i=0; i<numsSize; i++) {
        if ((nums[i]&diff)==0) {
            ans[0]^=nums[i];
        }
        else {
            ans[1]^=nums[i];
        }
    }
    *returnSize=2;
    return ans;
}
```

这个题和Single Number很像，可以用异或运算得到两个数进行按位异或之后的结果，所以关键就是把这两个数分开，可以将结果与其补码进行按位与运算，即diff&=-diff，
这样就将diff变成了仅有1个1，其它位置都为0的数，且那个1就是a和b第一个不相同的位置，这样就能区分开a和b了。把数组中的每一个数都与diff进行按位与运算，可以知道
直到相同的数一定与其中一个数进行异或运算，而两个特殊的数也一定不与同一个数进行运算，所以最终就可以得出结果。
