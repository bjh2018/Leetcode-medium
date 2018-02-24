Kth Largest Element in an Array
====

1.问题描述
-----

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.<br> 
For example,<br>
Given [3,2,1,5,6,4] and k = 2, return 5.<br> 
Note: <br>
You may assume k is always valid, 1 ≤ k ≤ array's length.<br>
给定一个数组，找出其中第K大的数，并且第K大的数一定存在。<br>

2.思路
----

把数组按照从大到小的顺序排列，返回index为k-1的值即可。<br>

3.代码I
----

```c
int findKthLargest(int* nums, int numsSize, int k) {
    int temp;
    for (int i=0; i<numsSize; i++) {
        for (int j=i+1; j<numsSize; j++) {
            if (nums[i]<nums[j]) {
                temp=nums[i];
                nums[i]=nums[j];
                nums[j]=temp;
            }
        }
    }
    return nums[k-1];
}
```

4.代码II
---

```c
void insertSort(int* nums, int len){
    for(int i = 1; i < len; i++){
        int tmp = *(nums+i);
        int j = i - 1;
        while(j>=0 && *(nums+j)<tmp){
            *(nums+j+1) = *(nums+j);
            j--;
        }//把当前的数字不断地与前面的比较，直到最后是的数组按从大到小的顺序排列
        *(nums+j+1) = tmp;
    }
}
int findKthLargest(int* nums, int numsSize, int k) {
    insertSort(nums, numsSize);
    return *(nums+k-1);
}
```

5.总结
---

可以利用指针解题减少运行时间，并且可以直接对数组进行改变。
