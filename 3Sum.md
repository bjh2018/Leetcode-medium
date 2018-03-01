3Sum
====

1.问题描述
----

Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.<br>
Note: The solution set must not contain duplicate triplets.<br>
For example, given array S = [-1, 0, 1, 2, -1, -4],<br>
<br>
A solution set is:<br>
[<br>
  [-1, 0, 1],<br>
  [-1, -1, 2]<br>
]<br>
给定一个数组，判断数组中是否存在三个数，这三个数相加和为0，如果存在，就把他们储存到一个二维数组中。

2.思路
---

解决三个数的相加的和是否为某一个值，就要知道这里面有三个变的量，一般就要用三个循环来解决，如果想要减少循环的次数，就要建立其中两个数之间的关系，就要把数组按照从小到大的顺序
排列，一个元素定住，把剩下两个元素一个是定住的元素的下一位，另一个是最后一位，然后查看三者的和，如果sum=0酒吧三个数储存起来，当sum是其他两种情况时再做出其他调整。为了避免重复
可以让三个元素分别与前一个或者后一个元素比较，如果重复，就加一或者减一，最终输出结果即可。<br>

3.代码
---

```c
void quickSort(int* nums,int first,int end){
    int temp,l,r;
    if(first>=end)return;
    temp=nums[first];
    l=first;r=end;
    while(l<r){
        while(l<r && nums[r]>=temp)r--;
        if(l<r)nums[l]=nums[r];
        while(l<r && nums[l]<=temp)l++;
        if(l<r)nums[r]=nums[l];
    }
    nums[l]=temp;
    quickSort(nums,first,l-1);
    quickSort(nums,l+1,end);
}
int** threeSum(int* nums, int numsSize, int* returnSize) {
    int i,sum,top=-1,begin,end;
    int** res=(int**)malloc(sizeof(int*)*(numsSize*(numsSize-1)*(numsSize-2))/6);
    if(numsSize<3){
        *returnSize=0;
        return res;
    }
    quickSort(nums,0,numsSize-1);
    for(i=0;i<numsSize;i++){
        if(nums[i]>0)break;
        if(i>0 && nums[i]==nums[i-1])continue;
        begin=i+1;end=numsSize-1;
        while(begin<end){
            sum=nums[i]+nums[begin]+nums[end];
            if(sum==0){
                top++;
	            res[top]=(int*)malloc(sizeof(int)*3);
              res[top][0]=nums[i];res[top][1]=nums[begin];res[top][2]=nums[end];
	            begin++;end--;
             while(begin<end && nums[begin]==nums[begin-1])begin++;
             while(begin<end && nums[end]==nums[end+1])end--;
            }else if(sum>0) end--;
            else begin++;
        }
    }
    *returnSize=top+1;
    return res;
}
```

4.总结
---

注意掌握这种两边都运用上的方法。
