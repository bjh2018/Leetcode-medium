Pow(x, n)
===

1.问题描述
-----

Implement pow(x, n). <br>
<br>
Example 1:<br> 
Input: 2.00000, 10<br>
Output: 1024.00000<br>
<br>
Example 2:<br> 
Input: 2.10000, 3<br>
Output: 9.26100<br>
求给定的数的n次方。

2.思路
-----

在一个循环中不断地把数连乘，得出结果。<br>

3.代码I(Time Limit Exceeded)
----

```c
double myPow(double x, int n) {
    long double result=1.0;
    int temp=0;
    if (n<0) {
        n=-n;
        temp=1;
    }
    if (n==0) return 1.0;
    else if (n>0) {
    for (int i=0; i<n; i++) {
        result=result*x;
    }
    }
    if (temp==1) {
        result=1.0/result;
    }
    return (double)result;
}
```

4.代码II
---

```c
double fastpow(double x, int n) {
    if (n==0) {
        return 1.0;
    }
    else if (n==1) {
        return x;
    }
    double ans=fastpow(x,n/2)*fastpow(x,n/2);
    if (n%2!=0) {
        ans=ans*x;
    }
    return ans;
}
double myPow(double x, int n) {
    if (n<0) {
        x=1.0/x;
        n=-n;
    }
    return fastpow(x,n);
}
```

这个代码的思路是：<br>
如果我们要求x的n次方，我们可以求x的n/2次方，以此类推就可以得到答案，要注意n为奇数的时候，少乘了一次x，要在最后再乘回来。写一个函数，并运用递归就可以得到答案。
这样就可以减少程序运行的时间。

5.代码III
---

```c
double myPow(double x, int n) {
    long long N=n;
    if (n<0) {
        x=1.0/x;
        N=-N;
    }
    double temp=x;
    double result=1;
   for (long long i=N; i; i=i/2) {
       if ((i%2)==1) {
           result=result*temp;
       }
       temp=temp*temp;//temp以2^n的速度增加
   }
    return result;
}
```

所求的结果可以根据x^(a+b)=x^a+x^b，把n写成二进制数，n用十进制就可以表示成好几个属相加，就可以通过幂指运算法则得到结果。
