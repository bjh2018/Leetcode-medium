 ZigZag Conversion
 =====
 
 1.问题描述
 -----
 
 The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility) <br>
 P   A   H   N<br>
 A P L S I I G<br>
 Y   I   R    <br>
And then read line by line: "PAHNAPLSIIGYIR"<br>
<br>
Write the code that will take a string and make this conversion given a number of rows:<br> 
string convert(string text, int nRows);<br>
convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".<br>
把一个字符串的各个字母按锯齿式排列之后，然后按照一行一行的顺序输出，所以解决这个问题的关键就是要找到新的字符串和原来的字符串之间的关系，可以发现第一行和最后一行的每个坐标之间都差sum个，而其他行都是
差一个随行数改变而改变的数。找到规律之后就可以把代码写出来了。

2.代码
---

```c
char* convert(char* s, int numRows) {
    int len=strlen(s);
    if (numRows<=1) return s;
    char* result=(char*)malloc(sizeof(char)*(len+1));
    memset(result,0,len);
    int u=0;
    int n=numRows;
    int sum=2*(n-1);
    for (int i=0; i<numRows; i++) {
        for (int j=i; j<len; j=j+sum) {
            result[u++]=s[j];
            int sec=(j-i)+sum-i;
            if (i!=0&&i!=numRows-1&&sec<len) {
                result[u++]=s[sec];
            }
        }
    }
    result[len]='\0';
    return result;
}
```

3.总结
----

要注意到字符串数组的最后一位一定式'\0'，所以就把新的字符串数组的最后一位设为'\0',而且要把申请空间之后的数组全部赋完值，以免出现错误。
