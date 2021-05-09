---
layout: post
title:  "LeetCode LinkedList Cycle 문제"
date: 2021-05-09
desc: "문제 풀이"
keywords: "Algrorithm, LinkedList, LinkedList Cycle"
categories: [Algorithm]
comments: true
tags: [C++, Algrorithm, LinkedList, LinkedList Cycle]
icon: icon-html
---

# LeetCode LinkedList Cycle

## LeetCode Top Interview Questions의 LinkedList 탭에 있는 PalindromeLinkedList를 풀어보았습니다.
  
### 주어진 문제에서 제한된 내용은
 - LinkedList의 Head가 주어졌을 때 해당 LinkedList가 Cycle을 가지는지 확인해주세요.
 - 노드 개수는 [0, 10^4] 사이의 값을 가집니다.
 - 노드의 값은 -10^5부터 10^5 사이의 값을 가집니다.
  
### 주어진 문제를 풀 때 중점적으로 봐야할 점.
 - 공간복잡도 O(1)으로 풀 수 있는지 확인해봅니다.
  
### 문제에서 주어진 ListNode  
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
```
  
### 풀이방식 방식
 - 포인터를 두개 사용하여, 포인터를 이동시키는데, 이동하는 개수를 한 포인터는 한개씩만 이동합니다.
 - 다른 한 포인터는 2개씩 이동합니다.
 - 이후 반복문을 돌다가 두 포인터가 같은 포인터를 가리키는 경우가 발생할 경우 순회하고 있다고 판단하고 true를 반환합니다. 
  
```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (head == NULL)
            return false;
        
        if (head->next == NULL)
            return false;
        
        ListNode *first = head;
        ListNode *sec = head;
        
        while (sec->next != NULL && sec->next->next != NULL)
        {
            first = first->next;
            sec = sec->next->next;
            if (first == sec)
            {
                return true;
            }
        }
        
        return false;
    }
};
```
