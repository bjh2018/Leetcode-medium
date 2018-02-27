Arithmetic Slices
======

1.问题描述
----

A sequence of number is called arithmetic if it consists of at least three elements and if the difference between any two consecutive elements is the same.<br>
For example, these are arithmetic sequence:<br>
1, 3, 5, 7, 9<br>
7, 7, 7, 7<br>
3, -1, -5, -9<br>
The following sequence is not arithmetic.<br>
1, 1, 2, 5, 7<br>
<br>
A zero-indexed array A consisting of N numbers is given. A slice of that array is any pair of integers (P, Q) such that 0 <= P < Q < N.<br>
A slice (P, Q) of array A is called arithmetic if the sequence:<br>
A[P], A[p + 1], ..., A[Q - 1], A[Q] is arithmetic. In particular, this means that P + 1 < Q.<br>
The function should return the number of arithmetic slices in the array A. <br>
<br>
Example: <br>
A = [1, 2, 3, 4]<br>
<br>
return: 3, for 3 arithmetic slices in A: [1, 2, 3], [2, 3, 4] and [1, 2, 3, 4] itself.<br>
给定的数组A中有几段相邻的元素的差距相同，序列的最短有三个元素，返回给定的数组中能构成的序列的个数。

2.思路
----

由题意可知序列最短有三个数，所以可以以3个元素为基础判断构成序列的基础，然后从第三个元素往后看下一个元素是否满足条件，同时记录下序列的长度。用序列的最大的长度得到子序列的个数
，因为差的距离是一定的，所以只要按着对长度进行不断地减一的操作，就可以得到结果。<br>

3。代码
-----

```c
int numberOfArithmeticSlices(int* A, int ASize) {
    int count=0;//切的片的数量
    int cha=0;//序列中各元素的差
    int len=0;//序列的长度
    int i=0, j=0;
    for ( i=0; i<ASize-2; i++) {
        if (A[i+1]-A[i]==A[i+2]-A[i+1]) {
            len=3;
            cha=A[i+1]-A[i];
            for (j=i+2; j<ASize-1; j++) {
                if (A[j+1]==A[j]+cha) {
                    len=len+1;
                }
                else break;
            }
            i=j;
    len=len-2;
    while(len>0) {
        count=count+len;
        len=len-1;
    }
        }
    }
    return count;
}
```

