Sort Colors
====

1.问题描述
----

Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.<br> 
Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively. <br>
Note:<br>
You are not suppose to use the library's sort function for this problem.<br>
给定一个数组，用数组中的数代表颜色，其中用0，1，2分别代表红色，白色和蓝色。把这组数按照红色，白色，蓝色的顺序排列。

2.思路
---

其实把这个题按纯数来看的话，就可以发现就是把数组按从小到大的顺序排列。

3.代码
----

```c
void sortColors(int* nums, int numsSize) {
    int temp=0;
    for (int i=0; i<numsSize; i++) {
        for (int j=i+1; j<numsSize; j++) {
            if (nums[i]>nums[j]) {
                temp=nums[i];
                nums[i]=nums[j];
                nums[j]=temp;
            }
        }
    }
}
```

