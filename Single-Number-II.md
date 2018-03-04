Single Number II
===

1.问题描述
----

Given an array of integers, every element appears three times except for one, which appears exactly once. Find that single one. <br>
给一个数组，数组中除了一个元素只出现一次，其他元素都出现了三次，找出只出现一次的数。

2.思路
---

在数组中的所有元素中，只出现一次的数是其中特殊的元素，就利用两个循环解决即可。

3.代码I
---

```c
int singleNumber(int* nums, int numsSize) {
    int temp=0, i;
    for ( i=0; i<numsSize; i++) {
        for (int j=0; j<numsSize; j++) {
            if (nums[i]==nums[j]) {
                temp++;
            }
        }
        if (temp==1) break;
        temp=0;
    }
    return nums[i];
}
```

4.代码II
---

```c
int singleNumber(int* nums, int numsSize) {
    int f[32];
    for (int i = 0; i < 32; ++i)
        f[i] = 0;
    for (int i = 0; i < numsSize; ++i) {
        int temp = nums[i];
        for (int j = 31; j >= 0; --j) {
            f[j] += temp&1;
            temp >>= 1;
        }
    }
    int result = 0;
    for (int i = 0; i < 32; ++i)
        result = result * 2 + f[i]%3;
    return result;
}
```

建立一个数组来储存给定数组的各个元素的各位上1的个数，再把得到的数除以3的余数，因为数组中的数除了单独的一个数只出现一次，所以肯定有1和0两种结果，再按二进制
转十进制的方法把结果换成十进制数即可，注意一开始是从最后一位找1的个数，而在转成十进制的时候顺序相反。
