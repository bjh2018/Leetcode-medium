 Maximum Product Subarray
 =====
 
 1.问题描述
 ---
 
 Find the contiguous subarray within an array (containing at least one number) which has the largest product. <br>
For example, given the array [2,3,-2,4],<br>
the contiguous subarray [2,3] has the largest product = 6.<br>
在数组中找到连续的子数组（至少包含一个数字），使得子数组的各个元素的乘积最大。

2.思路
---

子数组是连续的，说明子数组的开头不断的变化，如果从正向开始，把数组中的数不断的乘上，并且不断的取最大值，这样正向遍历，就可以改变反向遍历时的子数组的开头，
如果从最火以为开始不断地乘上数的话，就可以改变正向的子数组的开头，就可以找出答案。

3.代码
---

```c
int max(int x, int y) {
    if (x>y) return x;
    else return y;
}
int maxProduct(int* nums, int numsSize) {
    int begin=1, end=1;
    int ans=-2147483647;
    for (int i=0; i<numsSize; i++ ) {
        begin*=nums[i];
        end*=nums[numsSize-1-i];
        ans=max(ans, max(begin,end));
        begin=begin==0?1:begin;
        end=end==0?1:end;
    }
    return ans;
}
```

4.总结
---

连续的子数组有其特殊性，只要改变它的第一个元素和数组长度就可以得到不同的子数组，而在不断对其取最大的值的过程中就改变了它的长度，所以只要改变第一个元素
就可以，正向的第一个元素可以通过反向遍历时改变，反之，亦然。
