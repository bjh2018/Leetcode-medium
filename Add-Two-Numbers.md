Add Two Numbers
=======

1.问题描述
-----

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.
You may assume the two numbers do not contain any leading zero, except the number 0 itself.<br>
Example <br>
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)<br>
Output: 7 -> 0 -> 8<br>
Explanation: 342 + 465 = 807.<br>
有两个非空链表，表示两个非负整数。 数字以相反的顺序存储，每个节点都包含一个数字。 添加这两个数字并将其作为链接列表返回。<br>
假设这两个数字不包含任何前导零，除了数字0本身<br>

2.思路
------

就跟前面Add-Binary的思路一样，先取余，再除以时判断仅为的情况。而解决该问题的关键就是链表的创建<br>

3.代码
---

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* addTwoNumbers(struct ListNode* l1, struct ListNode* l2) {
    struct ListNode* ans=(struct ListNode*)malloc(sizeof(struct ListNode));//为ans申请空间
    struct ListNode* p=0;//链表头
    int temp=0,a,b,res=0;//temp是为了进位，a，b分别是两个链表中的整数，res是最终的结果
    while(l1!=0||l2!=0||temp!=0) {//之所以要让temp不为0时才停止循环是因为有可能最后一位要进位
       if (p==0) {
            p=ans;
        }
       else {
            p->next=(struct ListNode*)malloc(sizeof(struct ListNode));//申请空间
            p->next->val=0;//清一下
            p=p->next;
       }
        a=l1==0?0:l1->val;//如果l1为空的话，就让a=0
        b=l2==0?0:l2->val;
        res=(a+b+temp)%10;//如果把a，b换成l1->val和l2->val很容易造成错误，因为很有可能当一个为空时，另一个不是空，很容易超时
        temp=(a+b+temp)/10;
        p->val=res;
        p->next=0;//将链表的指针域指向空
        l1=l1==0?0:l1->next;
        l2=l2==0?0:l2->next;
    }
    return ans;
}
```
4.总结
----

链表<br>
（1）链表的构成：头指针(Header)，若干个节点(节点包括了数据域和指针域)，最后一个节点要指向空。<br>
（2）实现原理：头指针指向链表的第一个节点，然后第一个节点中的指针指向下一个节点，然后依次指到最后一个节点，这样就构成了一条链表。<br>
（3）链表的数据结构:<br>

```c
struct  list_node  
{  
    int data ; //数据域，用于存储数据  
    struct list_node *next ; //指针，可以用来访问节点数据，也可以遍历，指向下一个节点  
}; 
```

（4）创建链表

```c
list_single *create_list_node(int data)  
{  
    list_single *node = NULL ;  //1.定义一个头指针
    node = (list_single *)malloc(sizeof(list_single));  //2.然后分配内存空间
    if(node == NULL){  
        printf("malloc fair!\n");  
    }  
    memset(node,0,sizeof(list_single));  //3.清一下
    node->data = 100 ;  //4.给链表中的结点的数据赋值
    node->next = NULL ;  //5.将链表的指针域指向空
    return node ;  
}  

