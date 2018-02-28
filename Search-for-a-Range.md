Search for a Range
====

1.问题描述
----

Given an array of integers sorted in ascending order, find the starting and ending position of a given target value.<br>
Your algorithm's runtime complexity must be in the order of O(log n).<br>
If the target is not found in the array, return [-1, -1].<br>
For example,<br>
Given [5, 7, 7, 8, 8, 10] and target value 8,<br>
return [3, 4]. <br>
在按升序排列的数组中找到与target相等的数第一次出现和最后一次出现的index。

2.思路
---

对给定的数组进行遍历，把等于target的所有的输的index都保存在一个数组中，然后再建立一个数组，把第一个和最后一个index都保存到这个数组中，最后返回这个数组即可。
当数组中没有与target相等的数时，就返回[-1,-1]。<br>

3.代码I
---

```c
/**
 * Return an array of size *returnSize.
 * Note: The returned array must be malloced, assume caller calls free().
 */
int* searchRange(int* nums, int numsSize, int target, int* returnSize) {
    int *ans=(int *)malloc(sizeof(int)*numsSize);
    int temp=0;
    for (int i=0; i<numsSize; i++) {
        if (nums[i]==target) {
            ans[temp]=i;
            temp++;
        }
    }
    int *res=(int *)malloc(sizeof(int)*2);
    if (temp<1) {
        res[0]=-1;
        res[1]=-1;
    }
    else {
        res[0]=ans[0];
        res[1]=ans[temp-1];
    }
    *returnSize=2;
    return res;
}
```

4.代码II
---

```c
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] targetRange = {-1, -1};

        // find the index of the leftmost appearance of `target`.
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == target) {
                targetRange[0] = i;
                break;
            }
        }

        // if the last loop did not find any index, then there is no valid range
        // and we return [-1, -1].
        if (targetRange[0] == -1) {
            return targetRange;
        }

        // find the index of the rightmost appearance of `target` (by reverse
        // iteration). it is guaranteed to appear.
        for (int j = nums.length-1; j >= 0; j--) {
            if (nums[j] == target) {
                targetRange[1] = j;
                break;
            }
        }

        return targetRange;
    }
}
```

先从左边开始索引，直到遇到等于target的数就终止，然后再从右边开始索引，也是遇到target就终止，如果没有终止就证明不存在这样的数，所以可以先把要返回的数都
写成-1，如果经历一次循环后，值没有变，就说明不存在这样的数。

