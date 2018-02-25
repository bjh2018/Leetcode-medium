Battleships in a Board
====

1.问题描述
---

Given an 2D board, count how many battleships are in it. The battleships are represented with 'X's, empty slots are represented with '.'s. You may assume the following rules: <br>
You receive a valid board, made of only battleships or empty slots.<br>
Battleships can only be placed horizontally or vertically. In other words, they can only be made of the shape 1xN (1 row, N columns) or Nx1 (N rows, 1 column), where N can be of any size.<br>
At least one horizontal or vertical cell separates between two battleships - there are no adjacent battleships.<br>
Example:<br>
X..X<br>
...X<br>
...X<br>
In the above board there are 2 battleships.<br> 
Invalid Example:<br>
...X<br>
XXXX<br>
...X<br>
This is an invalid board that you will not receive - as battleships will always have a cell separating between them.<br> 
<br>
给定一个二维数组，用X代表战舰，其他空的地方用'.'来代表，而且战舰只能按一排或者一列来排列，没有相邻的战舰，战舰的水平或者垂直方向上至少相邻的有一个是'.'，找出给定的数组中战舰的数量。

2.思路
---

一开始看这道题，文字描述很多，本来是打算按行和按列两种情况来找出战舰的数量，并且保证相邻的是空格，但是却总是出错，其实再仔细研究题目，就会发现只要保证一行或者一列中有间隙地排列这战舰即可，而且不一定要同时看左边的
一个和后面的一个，只要是一行或者一列按一定的顺序即可，比如你按左边来看是不是战舰相邻，下次再遇到战舰时，就再看它左变是不是战舰就行。<br>

3.代码
----

```c
int countBattleships(char** board, int boardRowSize, int boardColSize) {
    int count = 0;
    for(int i=0;i<boardRowSize;i++)
        for(int j=0;j<boardColSize;j++)
            if(board[i][j]=='X' && (i==boardRowSize-1 || board[i+1][j]!='X') && (j==boardColSize-1 || board[i][j+1]!='X')) count++;
    return count;

}
```

4.总结
---

认真的分析题目是解决问题的关键，在理解透题目的基础上再写代码会容易得多。
