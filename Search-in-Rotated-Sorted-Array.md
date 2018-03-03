Search in Rotated Sorted Array
===

1.问题描述
----

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.<br>
(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).<br>
You are given a target value to search. If found in the array return its index, otherwise return -1.<br>
You may assume no duplicate exists in the array.<br>
已经排好序的一组数中在某点发生转变，如果数组中存在一个数等于target，就返回他的index,如果不存在，就返回-1。

2.思路
---

对数组进行遍历，看是否存在这样的数。

3.代码I
---

```c
int search(int* nums, int numsSize, int target) {
    for (int i=0; i<numsSize; i++) {
        if (nums[i]==target) {
            return i;
            break;
        }
    }
    return -1;
}
```

4.代码II
---

```c
int search(int* nums, int numsSize, int target) {
        int i = 0;
    if (numsSize<1){
        return -1;
    }
    while (i<numsSize){
        if (nums[i]==target){
                return i;
        }
        if(i>0){
            if (nums[i]<nums[i-1]){//不按照升序排列，转折点，说明nums[i-1]最大，nums[i]最小
                if (target>nums[i-1]){
                    return -1;
                }
                if (target<nums[i]){
                    return -1;
                }
            }
            else{//按照升序排列
                if ((target<nums[i])&&(target>nums[i-1])){//介于两个元素之间
                    return -1;
                }
            }
        }
        i++;
    }
    return -1;//当元素个数为1，i=0并且num[0]!=target时
    
}
```

利用了数组的特殊性。
