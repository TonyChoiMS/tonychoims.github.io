---
layout: post
title:  "C++ Linked List."
date: 2017-12-07
desc: "C++ 기반의 Linked List에 대한 정리 및 소스 코드"
keywords: "C++, LinkedList, Double LinkedList"
categories: [Programming]
comments: true
tags: [C++, LinkedList, Double LinkedList]
icon: icon-html
---

[최종 수정일 : 2021-04-29]

# __링크드리스트__
1. 데이터의 메모리주소의 순서가 순차적으로 이루어져있지 않다.
 - 1번 뒤에 2번이 있다는 보장이 없음
 - 노드(링크)에 의해 논리적으로 연결되어 있음.
2. Single LinkedList와 Double LinkedList 두종류로 존재함.
 - Double LinkedList의 경우엔 내 다음 노드(Next) 뿐만 아니라, 이전 노드(Prev)의 주소정보까지 가지고있음.
3. 임의 접근(Random Access)이 불가능함.
 - 현재의 노드가 알 수 있는 건 바로 내 다음의 노드의 존재만이기때문
4. 데이터 삽입/삭제에 있어서 강점이 있음
 - 물리적인 메모리 이동없이 요소간의 링크만 조작하면 되므로 속도에 유리.
 - 삽입할 위치의 이전 노드의 다음 노드포인터(Next)에 삽입할 노드를 연결하고, 삽입할 노드의 다음 노드포인터(Next)에 이전 노드의 Next에 저장되있던 포인터를 저장합니다.
 - 삭제 할 노드 앞 뒤를 서로 연결한 후, 삭제할 데이터의 노드를 삭제.
6. 메모리의 낭비가 없음
 - 배열의 형식처럼 미리 Size를 선언한 뒤, 사용하는 것이 아닌, 노드의 추가 / 삭제 할 때 메모리 할당을 하기 때문.
7. 한 노드에 여러개의 변수 또는 데이터값을 포함할 수 있다.
8. 다음 노드가 NULL을 가리킬 경우, 리스트의 끝(마지막 노드)이라는 뜻. 
<br />
// Single LinkedList 예시

~~~Cpp
#include <iostream>
#include "LinkedList.h"

using namespace std;

LinkedList::LinkedList() {
	head->nextNode = NULL;
	LinkedList::Count = 0;
}

LinkedList::~LinkedList() {
	
}

int LinkedList::get(int index) {
	try {
		valid(index);
	}
	catch (const char* msg) {
		cout << msg << endl;
		return -1;
	}
	Node* temp = head;
	for (int i = 0; i <= index; i++) {
		temp = temp->nextNode;
	}
	return temp->data;
}

void LinkedList::valid(int count) {
	if (count > LinkedList::Count) {
		throw "Error : À¯È¿ÇÏÁö ¾ÊÀº index";
	}
}

void LinkedList::add(int data) {
	Node* newNode = new Node;
	newNode->data = data;
	newNode->nextNode = NULL;

	if (head->nextNode == NULL) {
		head->nextNode = newNode;
	}
	else {
		Node* temp = head;
		while (temp->nextNode != NULL) {
			temp = temp->nextNode;
		}
		temp->nextNode = newNode;
	}
	LinkedList::Count++;
}

void LinkedList::add(int index, int data) {
	try {
		valid(index);
	}
	catch (const char* msg) {
		cout << msg << endl;
		return;
	}

	Node* newNode = new Node;
	newNode->data = data;
	newNode->nextNode = NULL;

	if (head->nextNode == NULL) {
		head->nextNode = newNode;
	}
	else {
		Node* temp = head;
		for (int i = 0; i < Count; i++) {
			temp = temp->nextNode;
		}
		newNode->nextNode = temp->nextNode;
		temp->nextNode = newNode;
	}
	LinkedList::Count++;
}

int LinkedList::size() {
	return LinkedList::Count;
}

void LinkedList::set(int index, int data) {
	try {
		valid(index);
	}
	catch (const char* msg) {
		cout << msg << endl;
		return;
	}

	Node* temp = head;
	for (int i = 0; i <= index; i++) {
		temp = temp->nextNode;
	}
	temp->data = data;
}

void LinkedList::remove(int index) {
	try {
		valid(index);
	}
	catch (const char* msg) {
		cout << msg << endl;
		return;
	}

	Node* temp = head;
	Node* remove = head;

	for (int i = 0; i < index; i++) {
		temp = temp->nextNode;
		remove = remove->nextNode;
	}
	remove = remove->nextNode;

	temp->nextNode = remove->nextNode;
	remove->nextNode = NULL;
	delete remove;
	LinkedList::Count++;
}

bool LinkedList::isEmpty() {
	Node* nodeHead = head;
	if (nodeHead->nextNode == NULL) {
		return true;
	}
	else {
		return false;
	}
}
~~~
<br />
예제 URL : https://github.com/TonyChoiMS/DataStructure/tree/master/DataStructureLib/DataStructureLib
