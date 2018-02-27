Total Hamming Distance
====

1.问题描述
----

The Hamming distance between two integers is the number of positions at which the corresponding bits are different.<br>
Now your job is to find the total Hamming distance between all pairs of the given numbers. <br>
Example:<br>
Input: 4, 14, 2<br>
<br>
Output: 6<br>
<br>
Explanation: In binary representation, the 4 is 0100, 14 is 1110, and 2 is 0010 (just
showing the four bits relevant in this case). So the answer will be:<br>
HammingDistance(4, 14) + HammingDistance(4, 2) + HammingDistance(14, 2) = 2 + 2 + 2 = 6.<br>
其实和Hamming Distance的不同就是是要把数组中的每个数与其他数都求一下距离，就想到要写一个函数，用来计算两个数之间的距离。

2.思路
---

首先用异或运算来把数转换，然后把数转成二进制，看二进制中一的个数即可。

3.代码I
-----

```c
int distance(int l, int r)  {
        long long k = l ^ r, res = 0;
        int temp=0;
        while (k>0) {
        temp=k%2;
        k=k/2;
        if (temp==1) {
            res++;
        }
    }
    return res;
    }
int totalHammingDistance(int* nums, int numsSize) {
   int answer=0,i=0;
    for (i=0; i<numsSize-1; i++) {
        for (int j=i+1; j<numsSize; j++) {
            answer=answer+distance(nums[i],nums[j]);
        }
    }
    return answer;
    }
```
代码的结果是超时，可以看出每次求两个数之间的距离的时候就要调用一次函数，而调用的函数中就有一次循环，如果是很大的数的话，循环的次数也会增多，就很容易造成超时。<br>

4.代码II
---

```c
int totalHammingDistance(int* nums, int numsSize) {
int i=0,j=0,count=0,distance=0;
    for(j=0;j<32;j++){
        for(i=0,count=0;i<numsSize;i++){
            count+=nums[i]&1;//如果最后一位是1，count就是1，反之就是0，也就是所有的数中相同的为上一的个数
            nums[i]=nums[i]>>1;//把当前的数右移一位，就可以判断第二位中一的个数
        }
        distance+=count*(numsSize-count);//1的个数乘以0的个数，因为每一个遇到1都会是1的个数增加
    }
    return distance;

}
```

这个代码是从整体的观念来，二进制数最多有32位，就一位一位地来看，最终加起来。

5.关于移位运算
------

 移位运算用来将整型或字符型数据作为二进位信息串作整体移动。有两个运算符：<br>
     << (左移) 和 >> (右移)<br>
移位运算是双目运算，有两个运算分量,左分量为移位数据对象，右分量的值为移位位数。移位运算将左运算分量视作由二进位组成的位串信息,对其作向左或向右移位，得到新的位串信息。<br>
    移位运算符的优先级低于算术运算符，高于关系运算符，它们的结合方向是自左至右。<br>
   (1)左移运算符(<<)<br>
    左移运算将一个位串信息向左移指定的位，右端空出的位用0补充。例如014<<2,结果为060,即48。<br>
    左移时，空出的右端用0补充，左端移出的位的信息就被丢弃。在二进制数运算中，在信息没有因移动而丢失的情况下，每左移1位相当于乘2。如4 << 2，结果为16。<br>
   (2)右移运算符(>>)<br>
    右移运算将一个位串信息向右移指定的位，右端移出的位的信息被丢弃。例如12>>2,结果为3。与左移相反，对于小整数，每右移1位，相当于除以2。在右移时，需要注意符号位问题。对无符号数据，右移时，左端空出的位用0补充。对于带符号的数据，如果移位前符号位为0(正数)，则左端也是用0补充；如果移位前符号位为1(负数)，则左端用0或用1补充，取决于计算机系统。对于负数右移，称用0 补充的系统为“逻辑右移”，用1补充的系统为“算术右移”。以下代码能说明读者上机的系统所采用的右移方法:<br>
     printf("%d\n\n\n", -2>>4);<br>
若输出结果为-1，是采用算术右移；输出结果为一个大整数，则为逻辑右移。<br>
