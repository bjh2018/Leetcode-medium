Remove Duplicates from Sorted List
===

1.问题描述
---

Given a sorted linked list, delete all duplicates such that each element appear only once.<br>
Example 1:<br>
Input: 1->1->2<br>
Output: 1->2<br>
Example 2:<br>
Input: 1->1->2->3->3<br>
Output: 1->2->3<br>
给定一个排序链表，删除所有重复项，以便每个元素只出现一次。

2.思路
---

在遍历的过程中，让一个指针p等于头指针，另一个q指向链表的第二个元素，然后开始遍历，如果这两个指针指向的val不同，那么就都向后移一个单位，如果相同的话，就让
p的下一位是q的下一位，然后让q移动到下一位，如此循环往复即可，注意要保证p存在。

3.代码I
---

```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* deleteDuplicates(struct ListNode* head) {
    if(!head) return NULL;
    struct ListNode*p=head;
    struct ListNode*q=head->next;
    while (p&&q) {
        if (p->val!=q->val) {
            p=q;
            q=q->next;
        }
        else {
           p->next=q->next;
            q=q->next;
        }
    }
    return head;
}
```

4.代码II
---

```c
struct ListNode* deleteDuplicates(struct ListNode* head) {
 struct ListNode* cur = head;
        
        while(cur) 
        {
        	while(cur->next && cur->val == cur->next->val)
            {
        		cur->next = cur->next->next;
        	}
        	cur = cur->next;
        }
        
        return head;
}
```

也可以只用一个指针，在链表中操作，比较当前元素与后一个元素的大小关系，如果相等的话，就把当前元素的下一位，设成他后面的后面的一位，如果不相等，就往后移一位，
再判断即可。
