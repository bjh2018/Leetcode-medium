Longest Substring Without Repeating Characters
============

1.问题描述
-----

Given a string, find the length of the longest substring without repeating characters.<br>
Examples:<br>
Given "abcabcbb", the answer is "abc", which the length is 3.<br>
Given "bbbbb", the answer is "b", with the length of 1.<br>
Given "pwwkew", the answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.<br>
给定一个字符串，找出其中最长的没有重复字母子字符串。<br>

2.思路
----

要想没有重复的字母，就要不断地进行比较，于是就要运用两个循环，一个循环是让字符串中的元素依次比较，另一个循环是让当前的字母与前面已经记录长度的元素进行比较，如果出现与先前的字母相同的字母，就先做一次比较把较长的长度留下，再把长度重置，结束这一次的循环，如果是不同，但是却并没有相邻，则长度不变。<br>

3.代码
-----

```c
int lengthOfLongestSubstring(char* s) {
   int max=1,len=0,length=1;//max是最终返回的最大的长度，len是当前元素的指数index，length是再遍历过程中出现的长度
   int i;
   while(s[len]) {
       if (len>=1) {//如果len是0的话，前面没有元素
           for (i=len-length; i<=len-1; i++) {//i<=len-1是指要把遍历的元素截到当前元素的前一个进行比较
               if (s[len]==s[i]) {//i=len-length是把起点改变，从不与当前元素相同的元素开始
                   if (max<length) {
                       max=length;
                   }//先把这一段长度进行比较之后，再进行下一段，因为不知道那一段长度最长
                   length=len-i;//把长度改成有效的长度
                   break;//跳出循环
               }
               else if (i==len-1) {//只有当当前元素与上一个元素不同时，才能把长度加1
                   length++;
                   if (max<length) {
                       max=length;
                   }
               }
           }
       }
       len++;
   }
    if (len==0) return 0;//如果len是0的话，说明字符串s中的长度为0
   return max;
}
```

4.总结
----

（1）一开始总是纠结如果从开始来找不同的元素的话，就会出现好多种情况要不断的比较，不知道该怎么把开始的点改变。可以用两个循环来实现对已经输出的长度的一段的检查，不断地往前面走。
（2）掌握求不重复的有效片段的方法：运用两个循环，一个输进元素，一个检查是否符合条件。注意起点改变的条件以及有效长度加1的条件。
