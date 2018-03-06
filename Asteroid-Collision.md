Asteroid Collision
===

1.问题描述
---

We are given an array asteroids of integers representing asteroids in a row. <br>
For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed. <br>
Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet. <br>
Example 1:<br>
Input: <br>
asteroids = [5, 10, -5]<br>
Output: [5, 10]<br>
Explanation: <br>
The 10 and -5 collide resulting in 10.  The 5 and 10 never collide.<br>
<br>
Example 2:<br>
Input: <br>
asteroids = [8, -8],<br>
Output: []<br>
Explanation: <br>
The 8 and -8 collide exploding each other.<br>
<br>
Example 3:<br>
Input: <br>
asteroids = [10, 2, -5]<br>
Output: [10]<br>
Explanation: <br>
The 2 and -5 collide resulting in -5.  The 10 and -5 collide resulting in 10.<br>
<br>
Example 4:<br>
Input: <br>
asteroids = [-2, -1, 1, 2]<br>
Output: [-2, -1, 1, 2]<br>
Explanation: <br>
The -2 and -1 are moving left, while the 1 and 2 are moving right.<br>
Asteroids moving the same direction never meet, so no asteroids will meet each other.<br>
<br>
Note: <br>
The length of asteroids will be at most 10000.<br>
Each asteroid will be a non-zero integer in the range [-1000, 1000]..<br>
给定一个数组，数组中数字的正负代表卫星运动的方向，数字的绝对值代表卫星的大小，两卫星相撞时，质量较大的留下，质量较小的消失，并且想装货留下的拿一个卫星也可能与它前一个卫星相撞。

2.思路
---

根据题意可以看出数组中不含0，所以就想到要把被撞毁的卫星的数值设为0，并且在进行比较时要保证比较的两个数都不为零，只要出先撞毁的情况，就重新开始遍历数组。（费时很长）

3.代码I
---

```c
int* asteroidCollision(int* asteroids, int asteroidsSize, int* returnSize) {
    int right=0;
    for (int left=0; left<asteroidsSize-1;left++) {
        while (asteroids[left]==0) {
            left++;
            if (left==asteroidsSize) {break;}
        }
        right=left+1;
        while (asteroids[right]==0) {
            right++;
            if (right==asteroidsSize) {break;}
        }
        if ((left==asteroidsSize)||(right==asteroidsSize)) {break;}
        if (asteroids[left]>0&&asteroids[right]<0) {
            if(asteroids[left]<-asteroids[right]) {
                asteroids[left]=asteroids[right];
            }
            else if (asteroids[left]==-asteroids[right]) {
                asteroids[left]=0;
            }
            asteroids[right]=0;
                left=-1;
        }   
    }
    int sum=0;
    for (int i=0; i<asteroidsSize; i++) {
        if (asteroids[i]!=0) {
            asteroids[sum++]=asteroids[i];
        }
    }
    *returnSize=sum;
    return asteroids;
}

4.代码II
---

```c
