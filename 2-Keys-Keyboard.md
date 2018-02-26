2 Keys Keyboard
====

1.问题描述
-----

Initially on a notepad only one character 'A' is present. You can perform two operations on this notepad for each step: <br>
Copy All: You can copy all the characters present on the notepad (partial copy is not allowed).<br>
Paste: You can paste the characters which are copied last time.<br>
<br>
Given a number n. You have to get exactly n 'A' on the notepad by performing the minimum number of steps permitted. Output the minimum number of steps to get n 'A'. <br>
Example 1:<br>
Input: 3<br>
Output: 3<br>
Explanation:<br>
Intitally, we have one character 'A'.<br>
In step 1, we use Copy All operation.<br>
In step 2, we use Paste operation to get 'AA'.<br>
In step 3, we use Paste operation to get 'AAA'.<br>
<br>
Note:<br>
The n will be in the range [1, 1000].<br>
现在只有一个A，给定一个整数n，可以通过复制全部和粘贴的操作，把A的数量增加到n，求得到n个A所需要的操作的步数的最小值。

2.思路
----

复制和粘贴是两步,并且进行一次复制之后粘贴的次数是不确定的，所以要用一个数来记录复制的步数，这样好把已经得到的步数再相加。

3.代码
----

```c
int minSteps(int n) {
    int ans=1;//当前A的个数
    int zou=0;//当前复制的步数
    int res=0;//当前走的总步数
    while(ans<n) {
        if (n%ans==0) {
            res=res+2;
            zou=ans;
            ans=ans+ans;
        }
        else {
            res=res+1;
            ans=ans+zou;
        }
    }
    return res;
}
```
