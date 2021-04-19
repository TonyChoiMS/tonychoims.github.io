---
layout: post
title:  "LeetCode PalindromeLinkedList 문제"
date: 2021-04-20
desc: "문제 풀이"
keywords: "Algrorithm", "Palindrome", "LinkedList"
categories: [Programming]
comments: true
tags: [Algrorithm, LinkedList, Palindrome]
icon: icon-html
---

### PalindromeLinkedList

## LeetCode Top Interview Questions의 LinkedList 탭에 있는 PalindromeLinkedList를 풀어보았습니다.
# 주어진 문제에서 제한된 내용은
 - 노드는 1부터 10^5까지의 개수를 가질 수 있습니다.
 - 노드의 value는 0 <= value <= 9 까지 가질 수 있습니다.

# 주어진 문제를 풀 때 중점적으로 봐야할 점.
 - 시간복잡도 O(n)과 공간복잡도 O(1)으로 풀 수 있는지 확인해봅니다.

# 문제에서 주어진 ListNode
~~~Cpp
struct ListNode 
{
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
    
};
~~~

# BrouteForce 방식
 - Palindrome은 뒤집어도 똑같은지 확인하는 알고리즘 이므로, 배열의 절반을 돌면서, 
 - 앞의 값과 뒤의 값이 같은지 확인하는 방법을 사용합니다.
 - 이 방법은 시간복잡도는 O(n)이 될 수 있으나, 공간복잡도도 O(n)이므로 문제에서 원하는 답은 아닙니다.
 - 심지어 LeetCode에 입력해본 결과 런타임 시간도 다른 사람에 비해 엄청 높음...
 - Runtime: 240 ms
 - Memory Usage : 128.2 MB

~~~Cpp
std::vector<int> vec;

bool Solution(ListNode* head)
{
    while (head != nullptr)
    {
        std::cout << "val : " << std::endl;
        vec.push_back(head->val);
        head = head->next;
    }

    int size = vec.size() / 2;
    std::cout << size << std::endl;
    for (int i = 0; i < size; i++)
    {
        if (vec[i] == vec[vec.size() - 1 - i])
            continue;
        else
            return false;
    }

    return true;
}
~~~

# 재귀호출을 이용한 방식
 - StackOverflow에서 소개한 방법 중 하나인데, 런타임 시간이 위에 했던 방식보다 오래걸림...
 - 재귀호출을 이용한 방식이라 한번 적용해봤습니다.
 - Runtime: 268 ms
 - Memory Usage : 146.2 MB

 ~~~Cpp
#include <funtional>

bool Solution(ListNode* head)
{
    std::function<bool(ListNode*)> ip_rec = [&](ListNode* p) -> bool
		{
			if (p)
			{
				if (!ip_rec(p->next)) return false;
				if (p->val != head->val) return false;
				head = head->next;
			}
			return true;
		};

		return ip_rec(head);
}
 ~~~

# LeetCode에서 발견한 풀이법
 - 포인터를 두개 사용하여, 포인터를 이동시키며 해당 값이 팰린드롬 인지 확인하는 방법입니다.
 - 재귀호출을 이용하여 노드를 뒤집는 방법까지 사용했습니다.
 ~~~Cpp

 ListNode* reverse(ListNode* head) 
 {
    if (head == nullptr || head->next == nullptr)
        return head;

    ListNode* rest_head = reverse(head->next);
    ListNode* rest_tail = head->next;

    rest_tail->next = head;
    head->next = nullptr;

    return rest_head;
}

bool Solution(ListNode* head)
{
    if (head == nullptr || head->next == nullptr)
        return true;

    ListNode* slow = head;
    ListNode* fast = head;

    while (fast != nullptr && fast->next != nullptr) 
    {
        fast = fast->next->next;
        if (fast != nullptr)
            slow = slow->next;
    }

    ListNode* rev = reverse(slow->next);
    ListNode* curr = head;

    while (rev != nullptr) 
    {
        if (curr->val != rev->val)
            return false;

        curr = curr->next;
        rev = rev->next;
    }

    return true;
}
~~~
