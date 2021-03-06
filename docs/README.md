# Data Structures in C++

Same Old Shite :joy: written, compiled & coded by [A2K](https://github.com/deadcoder0904)

## Linked List

Like arrays, Linked List is a linear data structure. Unlike arrays, linked list elements are not stored at contiguous location; the elements are linked using pointers.

## Singly Linked List

It points in only one direction

![linked-list](assets/img/linked-list.png)

### 1. Structure

```cpp

typedef char dataType;

typedef struct node {
	dataType data;
	struct node *next;
} node;

```

### 2. Print

```cpp

void printList(node *node) {
	
	if(node == NULL) {
		cout<<"The linked list is empty"<<endl;
		return;
	}

	while(node != NULL) {
		cout<<(node->data)<<" -> ";
		node = node->next;
	}
	cout<<"NULL";
}

```

### 3. Insertion

Insertion in a linked list can be done in 3 ways - 

#### A. Insert at Start

![linked-list-insertion-1](assets/img/linked-list-insertion-1.png)

```cpp

void insertAtStart(node **head, dataType data) {
	node* new_node = (node*) malloc(sizeof(node));
	
	new_node->data = data;
	new_node->next = *head;
	
	*head = new_node;
}

```

#### B. Insert after a Node

![linked-list-insertion-2](assets/img/linked-list-insertion-2.png)

```cpp

void insertAfter(node *prev_node, dataType data) {
	if(prev_node == NULL) {
		cout<<"Previous Node cannot be NULL"<<endl;
		return;
	}

	node* new_node = (node*) malloc(sizeof(node));
	
	new_node->data = data;
	new_node->next = prev_node->next;

	prev_node->next = new_node;
}

```

#### C. Insert in the end

![linked-list-insertion-3](assets/img/linked-list-insertion-3.png)

```cpp

void insertAtEnd(node **head, dataType data) {
	node* new_node = (node*) malloc(sizeof(node));
	
	new_node->data = data;
	new_node->next = NULL;

	if(*head == NULL) {
		*head = new_node;
		return;
	}

	node *last = *head;

	while(last -> next != NULL)
		last = last->next;
	
	last->next = new_node;
}

```

#### Example

```cpp

node *head = NULL;
insertAtEnd(&head, 'B');
insertAtFirst(&head, 'A');
insertAfter(head->next, 'C');
insertAtEnd(&head, 'D');
insertAtEnd(&head, 'E');
printList(head);

```

#### Output

<p class="tip">A -> B -> C -> D -> E -> NULL</p>

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/insert-a-node.cpp)

### 4. Deletion

#### A. Deleting a given key

![linked-list-deleting-a-given-key](./assets/img/linked-list-deleting-a-node.png)

```cpp

void deleteNodeWithSpecifiedKey(node **head, dataType key) {
	node *temp = *head, *prev;
	if(temp != NULL && temp->data == key) {
		*head = temp->next;
		free(temp);
		return;
	}

	while(temp != NULL && temp->data != key) {
		prev = temp;
		temp = temp->next;
	}

	if(temp == NULL) {
		cout<<"Key "<<key<<" not found"<<endl;
		return;
	}
	
	prev->next = temp->next;
	free(temp);
}

```

#### B. Deleting a key at given position

![linked-list-deleting-a-key-at-given-position](./assets/img/linked-list-deleting-at-given-position.png)

```cpp

void deleteNodeWithSpecifiedPostion(node **head,int position) {
	node *temp = *head;
	
	if(temp == NULL) 
		return;

	if(position == 0) {
		*head = temp->next;
		free(temp);
		return;
	}

	for(int i = 0; temp != NULL && i < position-1; i++) 
		temp = temp->next;
	
	if(temp == NULL || temp->next == NULL)
		return;

	node *next = temp->next->next;
	
	free(temp->next);
	temp->next = next;
}

```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
cout<<"Deleting node with key 'C' : "<<endl;
deleteNodeWithSpecifiedKey(&head, 'C');
printList(head);
cout<<"Deleting node at position 1 : "<<endl;
deleteNodeWithSpecifiedPostion(&head,1);
printList(head);

```

#### Output

```cpp
Deleting node with key 'C' : 
A -> B -> D -> NULL
Deleting node at position 1 : 
A -> D -> NULL

```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/delete-a-node.cpp)

### 5. Length

#### A. Iterative

```cpp

int iterativeLength(node *head) {
	int length = 0;
	node *temp = head;
	while(temp != NULL) {
		temp = temp->next;
		length++;
	}
	return length;
}

```

#### B. Recursive

```cpp

int recursiveLength(node *head) {
	if(head == NULL)
		return 0;
	return recursiveLength(head->next) + 1;	
}

```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
cout<<"Length of Linked List using Iterative Method : "<<iterativeLength(head)<<endl;
cout<<"Length of Linked List using Recursive Method : "<<recursiveLength(head)<<endl;

```

#### Output

```cpp
Length of Linked List using Iterative Method : 5
Length of Linked List using Recursive Method : 5

```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/length-of-linked-list.cpp)

### 6. Search

#### A. Iterative

```cpp

int iterativeSearch(node *head, dataType key) {
	node *temp = head;
	while(temp != NULL) {
		if(temp->data == key)
			return true;
		temp = temp->next;
	}
	return false;
}

```

#### B. Recursive

```cpp

int recursiveSearch(node *head, dataType key) {
	if(head == NULL)
		return false;
	if(head->data == key)
		return true;
	return recursiveSearch(head->next,key);
}

```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
cout<<"Search key in a Linked List using Iterative Method : "<<iterativeSearch(head,'C')<<endl;
cout<<"Search key in a Linked List using Recursive Method : "<<recursiveSearch(head,'Z')<<endl;

```

#### Output

```cpp
Search key in a Linked List using Iterative Method : 1
Search key in a Linked List using Recursive Method : 0

```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/search-in-linked-list.cpp)

### 7. Swap Nodes

![linked-list-swap-nodes](./assets/img/linked-list-swap-nodes.png)

```cpp

void swapNodes(node **head, dataType x, dataType y) {
	if(x == y) return;

	node *prevX = NULL, *currentX = *head;
	while(currentX != NULL && currentX->data != x) {
		prevX = currentX;
		currentX = currentX->next;
	}

	node *prevY = NULL, *currentY = *head;
	while(currentY != NULL && currentY->data != y) {
		prevY = currentY;
		currentY = currentY->next;
	}
	
	if(currentX == NULL || currentY == NULL) 
		return;

	if(prevX != NULL)
		prevX->next = currentY;
	else *head = currentY;

	if(prevY != NULL)
		prevY->next = currentX;
	else *head = currentX;

	node *temp = currentY->next;
	currentY->next = currentX->next;
	currentX->next = temp;
}

```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
cout<<"Before Swapping Nodes : "<<endl;
printList(head);
swapNodes(&head,'B','D');
cout<<"After Swapping Nodes : "<<endl;
printList(head);

```

#### Output

```cpp
Before Swapping Nodes : 
A -> B -> C -> D -> E -> NULL
After Swapping Nodes : 
A -> D -> C -> B -> E -> NULL

```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/swap-nodes-in-linked-list.cpp)

### 8. Get Nth Node

```cpp
dataType getNthNode(node *head, int n) {
	node *temp = head;
	int count = 0;

	while(temp != NULL) {
		if(count == n)
			return temp->data;
		count++;
		temp = temp->next;
	}

	return '0';
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
cout<<"Get 2nd Node : "<<getNthNode(head,1)<<endl;

```

#### Output

```cpp
A -> B -> C -> D -> E -> NULL
Get 2nd Node : B

```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/get-nth-node.cpp)

### 9. Get Middle Node

#### A. Method One

```cpp
dataType getMiddleNode1(node *head) {
	if(head == NULL)
		return '0';

	int count = 0;
	node *temp = head;
	
	for(count = 0; temp != NULL; count++) 
		temp = temp->next;
	
	temp = head;
	
	for(int i = 0; i < count/2; i++)
		temp = temp->next;
	
	return temp->data;
}
```

#### B. Method Two

```cpp
dataType getMiddleNode2(node *head) {
	if(head == NULL)
		return '0';

	node *slow_ptr = head, *fast_ptr = head;

	while(fast_ptr != NULL && fast_ptr->next != NULL ) {
		slow_ptr = slow_ptr->next;
		fast_ptr = fast_ptr->next->next;
	}

	return slow_ptr->data;
}
```

#### C. Method Three

```cpp
dataType getMiddleNode3(node *head) {
	if(head == NULL)
		return '0';
	
	node *mid = head;
	
	for(int count = 0; head != NULL; count++) {
		if(count & 1)
			mid = mid->next;
		head = head->next;
	}
	
	return mid->data;
}
```

#### Example

```cpp
node *head = NULL;
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
cout<<"Get Middle Node 1 : "<<getMiddleNode1(head)<<endl;
cout<<"Get Middle Node 2 : "<<getMiddleNode2(head)<<endl;
cout<<"Get Middle Node 3 : "<<getMiddleNode3(head)<<endl;

```

#### Output

```cpp
A -> B -> C -> D -> E -> NULL
Get Middle Node 1 : C
Get Middle Node 2 : C
Get Middle Node 3 : C
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/print-middle-of-linked-list.cpp)

### 10. Get Nth Node from End

```cpp
dataType getNthNodeFromLast(node *head, int n) {
	node *temp = head;
	int len;
	
	for(len = 0; temp != NULL; len++)
		temp = temp->next;

	if(len < n)
		return '0';
	
	temp = head;
	for(int i = 0; i < len - n; i++)
		temp = temp->next;
	
	return temp->data;
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
cout<<"Get 2nd Node From Last : "<<getNthNodeFromLast(head,2)<<endl;

```

#### Output

```cpp
A -> B -> C -> D -> E -> NULL
Get 2nd Node From Last : D

```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/get-nth-node-from-last.cpp)

### 11. Delete Linked List

```cpp
void deleteLinkedList(node **head) {
	node *current = *head, *next;
	
	while(current != NULL) {
		next = current->next;
		free(current);
		current = next;
	}

	*head = NULL;
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
deleteLinkedList(&head);
printList(head);

```

#### Output

```cpp
The linked list is empty
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/delete-linked-list.cpp)

### 12. Frequency of a node

```cpp
int frequencyOfNode(node *head, dataType key) {
	int count = 0;
	while(head != NULL) {
		if(head->data == key)
			count++;
		head = head->next;
	}
	return count;
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
insertAtStart(&head, 'A');
insertAtStart(&head, 'F');
insertAtStart(&head, 'A');
insertAtStart(&head, 'C');
insertAtStart(&head, 'A');
insertAtStart(&head, 'B');
insertAtStart(&head, 'C');
insertAtStart(&head, 'A');
insertAtStart(&head, 'A');
printList(head);
cout<<"Node 'A' appeared "<<frequencyOfNode(head,'A')<<" times"<<endl;

```

#### Output

```cpp
A -> A -> C -> B -> A -> C -> A -> F -> A -> D -> E -> NULL
Node 'A' appeared 5 times
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/frequency-of-a-node.cpp)

### 13. Reverse linked List

#### A. Iterative

```cpp

void iterativeReverse(node **head) {
	node *prev = NULL, *current = *head, *next;
	
	while(current != NULL) {
		next = current->next;
		current->next = prev;
		prev = current;
		current = next;
	}
	
	*head = prev;
}

```

#### B. Recursive

```cpp

void recursiveReverse(node **head) {
	node *first, *rest;
	
	if(*head == NULL)
		return;

	first = *head;
	rest = first->next;

	if(rest == NULL)
		return;

	recursiveReverse(&rest);

	first->next->next = first;
	first->next = NULL;

	*head = rest;
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
iterativeReverse(&head);
printList(head);
recursiveReverse(&head);
printList(head);
```

#### Output

```cpp
A -> B -> C -> NULL
C -> B -> A -> NULL
A -> B -> C -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/reverse-linked-list.cpp)

### 14. Detect Loop

```cpp
int detectLoop(node *head) {
	node *slow_ptr = head, *fast_ptr = head;
	while(fast_ptr != NULL && fast_ptr->next != NULL) {
		slow_ptr = slow_ptr->next;
		fast_ptr = fast_ptr->next->next;
		if(slow_ptr == fast_ptr)
			return 1;
	}
	return 0;
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
head->next->next = head;
int loop = detectLoop(head);
if(loop)
	cout<<"Loop detected"<<endl;
else
	cout<<"Loop not detected"<<endl;
```

#### Output

```cpp
Loop detected
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/find-loop-in-linked-list.cpp)

### 15. Merge 2 sorted Linked List

#### A. Iterative

```cpp

node* iterativeMergeSort(node *x, node *y) {
	node *head = NULL;
	while(x != NULL && y != NULL) {
		if(x->data <= y->data) {
			insertAtEnd(&head,x->data);
			x = x->next;
		}
		else {
			insertAtEnd(&head,y->data);
			y = y->next;
		}
	}
	if(x == NULL) 
		while(y != NULL) {
			insertAtEnd(&head,y->data);
			y = y->next;	
		}
	else 
		while(x != NULL) {
			insertAtEnd(&head,x->data);
			x = x->next;	
		}	

	return head;
}

```

#### B. Recursive

```cpp

node* recursiveMergeSort(node *x, node *y) {
	node *head = NULL;

	if(x == NULL) return y;
	if(y == NULL) return x;

	if(x->data <= y->data) {
		head = x;
		head->next = recursiveMergeSort(head->next,y);
	}
	else {
		head = y;
		head->next = recursiveMergeSort(x,head->next);
	}
	return head;
}

```

#### Example

```cpp

node *head1 = NULL;
insertAtEnd(&head1, 'A');
insertAtEnd(&head1, 'B');
cout<<"1st linked list is :"<<endl;
printList(head1);

node *head2 = NULL;
insertAtEnd(&head2, 'E');
insertAtEnd(&head2, 'F');
insertAtEnd(&head2, 'G');
cout<<"2nd linked list is :"<<endl;
printList(head2);

cout<<"Iteratively Merged linked list is :"<<endl;
node *head3 = iterativeMergeSort(head1, head2);
printList(head3);

cout<<"Recursively Merged linked list is :"<<endl;
head3 = recursiveMergeSort(head1, head2);
printList(head3);
```

#### Output

```cpp
1st linked list is :
A -> B -> NULL
2nd linked list is :
E -> F -> G -> NULL
Iteratively Merged linked list is :
A -> B -> E -> F -> G -> NULL
Recursively Merged linked list is :
A -> B -> E -> F -> G -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/merge-two-sorted-linked-list.cpp)

### 16. Insert Node in a Sorted List

```cpp
void sortedInsert(node **head, dataType data) {
	if(*head == NULL) return;
	
	node*temp = *head;
	node* new_node = (node*) malloc(sizeof(node));
	new_node->data = data;

	if(temp->data > new_node->data) {
		new_node->next = temp;
		*head = new_node;
		return;
	}

	while(temp != NULL && temp->next != NULL) {
		if(temp->next->data > data) {
			new_node->next = temp->next;
			temp->next = new_node;
			break;
		}
		temp = temp->next;
	}
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'F');
insertAtStart(&head, 'E');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
sortedInsert(&head, 'D');
printList(head);
```

#### Output

```cpp
A -> B -> C -> E -> F -> NULL
A -> B -> C -> D -> E -> F -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/insert-node-in-sorted-list.cpp)

### 17. Delete Node given only Pointer to Node

```cpp
void deleteNodeOnlyGivenPointerToNode(node* ptr) {
	node* temp = ptr->next;
	ptr->data = temp->data;
	ptr->next = temp->next;
	free(temp);
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'F');
insertAtStart(&head, 'E');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
deleteNodeOnlyGivenPointerToNode(head);
printList(head);
```

#### Output

```cpp
A -> B -> C -> E -> F -> NULL
B -> C -> E -> F -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/delete-node-only-given-pointer-to-node.cpp)

<p class="warning">
	This solution doesn’t work if the node to be deleted is the last node of the list.
</p>

### 18. Palindrome

```cpp
node* cloneLinkedListInReverse(node *temp) {
	node *reverse = NULL;
	while(temp != NULL) {
		insertAtStart(&reverse,temp->data);
		temp = temp->next;
	}
	return reverse;
}

int isPalindrome(node *head1,node *head2) {
	while(head1 != NULL && head2 != NULL)
		if(head1->data != head2->data)
			return 0;
		else {
			head1 = head1->next;
			head2 = head2->next;
		}
	return 1;
}
```

#### Example

```cpp

node *head1 = NULL;
insertAtStart(&head1, 'R');
insertAtStart(&head1, 'A');
insertAtStart(&head1, 'D');
insertAtStart(&head1, 'A');
insertAtStart(&head1, 'R');

cout<<"1st Linked List : "<<endl;
printList(head1);

node *head2 = cloneLinkedListInReverse(head1);

cout<<"2nd Linked List : "<<endl;
printList(head2);

int palindrome = isPalindrome(head1,head2);

if(palindrome)
	cout<<"Palindrome"<<endl;
else cout<<"Not Palindrome"<<endl;
```

#### Output

```cpp
1st Linked List : 
R -> A -> D -> A -> R -> NULL
2nd Linked List : 
R -> A -> D -> A -> R -> NULL
Palindrome
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/check-if-linked-list-is-palindrome.cpp)

### 19. Recursive Print List

```cpp

void recursiveReversePrintList(node *head) {
	if(head == NULL) return;
	recursiveReversePrintList(head->next);
	cout<<head->data<<" ->";
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
recursiveReversePrintList(head);
cout<<"NULL";
```

#### Output

```cpp
A -> B -> C -> NULL
C -> B -> A -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/print-recursively-reverse-linked-list.cpp)

### 20. Remove Duplicates from sorted list

```cpp

void removeDuplicatesFromSortedList(node *head) {
	if(head == NULL)
		return;

	node *next_ptr;

	while(head->next != NULL)
		if(head->data == head->next->data) {
			next_ptr = head->next->next;
			free(head->next);
			head->next = next_ptr;
		}
		else
			head = head->next;
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
insertAtStart(&head, 'A');
insertAtStart(&head, 'A');
printList(head);
removeDuplicatesFromSortedList(head);
printList(head);
```

#### Output

```cpp
A -> A -> A -> B -> B -> C -> D -> D -> E -> NULL
A -> B -> C -> D -> E -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/remove-duplicates-from-sorted-linked-list.cpp)

### 21. Remove Duplicates from unsorted list

#### A. Iterative 

```cpp

void removeDuplicatesFromUnsortedList(node *head) {
	if(head == NULL)
		return;

	node *fixed = head, *moving;
	while(fixed != NULL && fixed->next != NULL) {
		moving = fixed;
		while(moving->next != NULL) {
			if(fixed->data == moving->next->data) {
				node *next_ptr = moving->next;
				moving->next = next_ptr->next;
				free(next_ptr);
			}
			else moving = moving->next;
		}
		fixed = fixed->next;
	}
}
```
#### B. Hashing 

```cpp

void removeDuplicatesFromUnsortedListUsingHashing(node *head) {
	unordered_set<int> seen;
	node *current = head, *prev = NULL;
	while(current != NULL) {
		if(seen.find(current->data) != seen.end()) {
			prev->next = current->next;
			free(current);
		}
		else {
			seen.insert(current->data);
			prev = current;
		}
		current = prev->next;
	}
}
```
#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'C');
insertAtStart(&head, 'A');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
insertAtStart(&head, 'A');
printList(head);
removeDuplicatesFromUnsortedList(head);
printList(head);
insertAtStart(&head, 'C');
insertAtStart(&head, 'A');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
insertAtStart(&head, 'A');
removeDuplicatesFromUnsortedListUsingHashing(head);
printList(head);
```

#### Output

```cpp
A -> A -> B -> A -> C -> NULL
A -> B -> C -> NULL
A -> B -> C -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/remove-duplicates-from-unsorted-linked-list.cpp)

### 22. Swap Pairs

```cpp

void swap(dataType *a, dataType *b) {
	dataType temp = *a;
	*a = *b;
	*b = temp;
}
```
#### A. Iterative 

```cpp

void swapPairsIterative(node *head) {
	if(head == NULL) return;

	while(head != NULL && head->next != NULL) {
		swap(&(head->data),&(head->next->data));
		head = head->next->next;
	}
}
```
#### B. Recursive 

```cpp

void swapPairsRecursive(node *head) {
	if(head == NULL || head->next == NULL) return;
	
	swap(&(head->data),&(head->next->data));
	swapPairsRecursive(head->next->next);
}
```
#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'F');
insertAtStart(&head, 'E');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
swapPairsIterative(head);
printList(head);
swapPairsRecursive(head);
printList(head);
```

#### Output

```cpp
A -> B -> C -> E -> F -> NULL
B -> A -> E -> C -> F -> NULL
A -> B -> C -> E -> F -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/swap-data-of-adjacent-pairs.cpp)

### 23. Move Last to First

```cpp

void moveLastToFirst(node **head) {
	if(*head == NULL) return;

	node *last = *head, *prev = NULL;

	while(last->next != NULL) {
		prev = last;
		last = last->next;
	}
	prev->next = NULL;
	last->next = *head;
	*head = last;
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'F');
insertAtStart(&head, 'E');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
moveLastToFirst(&head);
printList(head);
```

#### Output

```cpp
A -> B -> C -> E -> F -> NULL
F -> A -> B -> C -> E -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/move-last-element-to-first.cpp)

### 24. Intersection of 2 Sorted Lists

#### A. Dummy Head Node 

```cpp

node* intersectionOfTwoSortedListsUsingDummyNode(node *head1, node *head2) {
	node head, *tail = &head;
	head.next = NULL;
	while(head1 != NULL && head2 != NULL) {
		if(head1->data == head2->data) {
			insertAtEnd(&tail->next,head1->data);
			tail = tail->next;
			head1 = head1->next;
			head2 = head2->next;
		}
		else if(head1->data < head2->data)
					head1 = head1->next;
				else head2 = head2->next;
	}
	return head.next;
}
```

#### B. Pointer of Pointer 

```cpp

node* intersectionOfTwoSortedListsUsingPointerOfPointer(node *head1, node *head2) {
	node *head = NULL, **tail = &head;
	while(head1 != NULL && head2 != NULL) {
		if(head1->data == head2->data) {
			insertAtEnd(tail,head1->data);
			tail = &((*tail)->next);
			head1 = head1->next;
			head2 = head2->next;
		}
		else if(head1->data < head2->data)
					head1 = head1->next;
				else head2 = head2->next;
	}
	return head;
}
```

#### C. Recursion

```cpp

node* intersectionOfTwoSortedListsUsingRecursion(node *head1, node *head2) {
	if(head1 == NULL || head2 == NULL) return NULL;

	if(head1->data < head2->data)
		return intersectionOfTwoSortedListsUsingRecursion(head1->next, head2);

	if(head1->data > head2->data)
		return intersectionOfTwoSortedListsUsingRecursion(head1, head2->next);
	
	node *new_node = (node *)malloc(sizeof(node));
	new_node->data = head1->data;

	new_node->next = intersectionOfTwoSortedListsUsingRecursion(head1->next, head2->next);
	return new_node;
}
```

#### Example

```cpp

node *head1 = NULL;
insertAtEnd(&head1, 'A');
insertAtEnd(&head1, 'B');
insertAtEnd(&head1, 'C');
insertAtEnd(&head1, 'D');
insertAtEnd(&head1, 'E');
cout<<"1st linked list : "<<endl;
printList(head1);
node *head2 = NULL;
insertAtEnd(&head2, 'C');
insertAtEnd(&head2, 'D');
insertAtEnd(&head2, 'E');
cout<<"2nd linked list : "<<endl;
printList(head2);
node *head3 = intersectionOfTwoSortedListsUsingDummyNode(head1,head2);
cout<<"Intersection using Dummy Node : "<<endl;
printList(head3);
node *head4 = intersectionOfTwoSortedListsUsingPointerOfPointer(head1,head2);
cout<<"Intersection using Pointer of Pointer : "<<endl;
printList(head4);
node *head5 = intersectionOfTwoSortedListsUsingRecursion(head1,head2);
cout<<"Intersection using Recursion : "<<endl;
printList(head5);
```

#### Output

```cpp
1st linked list : 
A -> B -> C -> D -> E -> NULL
2nd linked list : 
C -> D -> E -> NULL
Intersection using Dummy Node : 
C -> D -> E -> NULL
Intersection using Pointer of Pointer : 
C -> D -> E -> NULL
Intersection using Recursion : 
C -> D -> E -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/intersection-of-two-sorted-lists.cpp)

### 25. Delete Alternate Nodes

#### A. Iterative 

```cpp

void deleteAlternateNodesIterative(node *head) {
	node *current = head, *next_ptr;

	while(current != NULL && current->next != NULL) {
		next_ptr = current->next;
		current->next = next_ptr->next;
		free(next_ptr);
		current = current->next;
	}
}
```
#### B. Recursive 

```cpp

void deleteAlternateNodesRecursive(node *head) {
	if(head == NULL || head->next == NULL) return;

	node *next_ptr = head->next;
	head->next = next_ptr->next;
	free(next_ptr);
	deleteAlternateNodesRecursive(head->next);
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
cout<<"Delete Alternate Nodes Iteratively : "<<endl;
deleteAlternateNodesIterative(head);
printList(head);
cout<<"Delete Alternate Nodes Recursively : "<<endl;
deleteAlternateNodesRecursive(head);
printList(head);
```

#### Output

```cpp
A -> B -> C -> D -> E -> NULL
Delete Alternate Nodes Iteratively : 
A -> C -> E -> NULL
Delete Alternate Nodes Recursively : 
A -> E -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/delete-alternate-node-of-linked-list.cpp)

### 26. Splitting Alternate Nodes

```cpp

void alternateSplitting(node *head, node **x, node **y) {
	if(head == NULL) return;
	
	for(int count = 1; head != NULL; count++) {
		if(count & 1)
			insertAtEnd(x, head->data);
		else insertAtEnd(y, head->data);
		head = head->next;
	}
}
```

#### Example

```cpp

node *head = NULL;
insertAtEnd(&head, 'A');
insertAtEnd(&head, 'B');
insertAtEnd(&head, 'C');
insertAtEnd(&head, 'D');
insertAtEnd(&head, 'E');
printList(head);
cout<<"Alternate Splitting of Linked List : "<<endl;
node *x = NULL, *y = NULL;
alternateSplitting(head, &x, &y);
printList(x);
printList(y);
```

#### Output

```cpp
A -> B -> C -> D -> E -> NULL
Alternate Splitting of Linked List : 
A -> C -> E -> NULL
B -> D -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/alternate-splitting-of-linked-list.cpp)

### 27. Identical Linked Lists

#### A. Iterative

```cpp

bool identicalLinkedListsIterative(node *x, node *y) {
	while(x != NULL && y != NULL) {
		if(x->data != y->data)
			return false;
		x = x->next;
		y = y->next;
	}
	
	return x == NULL && y == NULL;
}
```

#### B. Recursive

```cpp

bool identicalLinkedListsRecursive(node *x, node *y) {
	if(x == NULL && y == NULL) return true;

	if(x != NULL && y != NULL) 
		return (x->data == y->data) && identicalLinkedListsRecursive(x->next,y->next);
	return false;
}
```
#### Example

```cpp

node *x = NULL;
insertAtStart(&x, 'A');
insertAtStart(&x, 'B');
insertAtStart(&x, 'C');
insertAtStart(&x, 'D');
insertAtStart(&x, 'E');
cout<<"Linked List 1 : "<<endl;
printList(x);

node *y = NULL;
insertAtStart(&y, 'A');
insertAtStart(&y, 'B');
insertAtStart(&y, 'C');
insertAtStart(&y, 'D');
insertAtStart(&y, 'E');
cout<<"Linked List 2 : "<<endl;
printList(y);

cout<<"Iterative Method - "<<endl;
if(identicalLinkedListsIterative(x,y))
	cout<<"Linked Lists are Identical"<<endl;
else cout<<"Linked Lists are Not Identical"<<endl;

cout<<"Recursive Method - "<<endl;
if(identicalLinkedListsRecursive(x,y))
	cout<<"Linked Lists are Identical"<<endl;
else cout<<"Linked Lists are Not Identical"<<endl;
```

#### Output

```cpp
Linked List 1 : 
E -> D -> C -> B -> A -> NULL
Linked List 2 : 
E -> D -> C -> B -> A -> NULL
Iterative Method - 
Linked Lists are Identical
Recursive Method - 
Linked Lists are Identical
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/identical-linked-lists.cpp)

### 28. Merge Sort

```cpp

void FrontBackSplit(node *head, node **x, node **y) {	
	if(head == NULL || head->next == NULL) {
		*x = head;
		*y = NULL;
		return;
	}

	node *slow = head, *fast = head->next;

	while(fast != NULL) {
		fast = fast->next;
		if(fast != NULL) {
			slow = slow->next;
			fast = fast->next;
		}
	}

	*x = head;
	*y = slow->next;
	slow->next = NULL;
}

void mergeSort(node **headRef) {
	node *head = *headRef;
	
	if(head == NULL || head->next == NULL) return;

	node *x, *y;
	FrontBackSplit(head,&x,&y);
	mergeSort(&x);
	mergeSort(&y);
	*headRef = iterativeMergeSort(x,y);
}

```

#### Example

```cpp

node *head = NULL;
insertAtEnd(&head, 'F');
insertAtEnd(&head, 'E');
insertAtEnd(&head, 'C');
insertAtEnd(&head, 'B');
insertAtEnd(&head, 'A');
printList(head);
mergeSort(&head);
printList(head);
```

#### Output

```cpp
F -> E -> C -> B -> A -> NULL
A -> B -> C -> E -> F -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/merge-sort-for-linked-lists.cpp)

### 29. Reverse a list in Groups of Given Size

```cpp

node* reverseInGroups(node *head, int n) {
	node *current = head, *prev = NULL, *next = NULL;
	for(int i = 0; current != NULL && i < n; i++) {
		next = current->next;
		current->next = prev;
		prev = current;
		current = next;
	}
	
	if(next != NULL)
		head->next = reverseInGroups(next,n);

	return prev;
}

```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
insertAtStart(&head, 'C');
insertAtStart(&head, 'D');
insertAtStart(&head, 'E');
printList(head);
printList(reverseInGroups(head,3));
```

#### Output

```cpp

E -> D -> C -> A -> B -> NULL
C -> D -> E -> B -> A -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/reverse-linked-list-in-groups-of-given-size.cpp)

### 30. Alternate Reverse a list in Groups of Given Size

```cpp

node* alternateReverseInGroups(node *head, int n) {
	node *current = head, *prev = NULL, *next = NULL;
	for(int i = 0; current != NULL && i < n; i++) {
		next = current->next;
		current->next = prev;
		prev = current;
		current = next;
	}

	if(head != NULL)
		head->next = current;

	for(int i = 0; current != NULL && i < n-1; i++)
		current = current->next;
	
	if(current != NULL)
		current->next = alternateReverseInGroups(current->next,n);

	return prev;
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'J');
insertAtStart(&head, 'I');
insertAtStart(&head, 'H');
insertAtStart(&head, 'G');
insertAtStart(&head, 'F');
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
printList(alternateReverseInGroups(head,3));
```

#### Output

```cpp
A -> B -> C -> D -> E -> F -> G -> H -> I -> J -> NULL
C -> B -> A -> D -> E -> F -> I -> H -> G -> J -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/alternate-reverse-linked-list-in-groups-of-given-size.cpp)

### 31. Delete Nodes Having Greater Value on Right Side

```cpp

void delNodes(node *head) {
	node *current = head;
	while(current != NULL && current->next != NULL)
		if(current->next->data < current->data) {
			node *temp = current->next;
			current->next = temp->next;
			free(temp);
		}
		else current = current->next;
}

void deleteNodesHavingGreaterValueOnRightSide(node **head) {
	if(*head == NULL) return;

	iterativeReverse(head);
	delNodes(*head);
	iterativeReverse(head);
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'E');
printList(head);
deleteNodesHavingGreaterValueOnRightSide(&head);
printList(head);
```

#### Output

```cpp
E -> C -> D -> A -> B -> NULL
E -> D -> B -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/delete-nodes-which-have-greater-value-on-right-side.cpp)

### 32. Segregate Even & Odd Nodes

```cpp

void segregateEvenAndOdd(node **head) {
	if(*head == NULL) return;

	node *temp = *head, *even = NULL, *odd = NULL;
	while(temp != NULL) {
		if(temp->data & 1)
			insertAtEnd(&odd,temp->data);
		else insertAtEnd(&even,temp->data);
		temp = temp->next;
	}

	if(even == NULL) {
		*head = odd;
		return;
	}

	temp = even;
	while(temp->next != NULL)
		temp = temp->next;
	
	temp->next = odd;
	*head = even;	
}
```

#### Example

```cpp

node *head = NULL;
insertAtEnd(&head, 'B');
insertAtEnd(&head, 'A');
insertAtEnd(&head, 'C');
insertAtEnd(&head, 'D');
insertAtEnd(&head, 'E');
printList(head);
segregateEvenAndOdd(&head);
printList(head);
```

#### Output

```cpp
B -> A -> C -> D -> E -> NULL
B -> D -> A -> C -> E -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/segregate-even-odd-nodes-in-linked-list.cpp)

### 33. Find and Remove Loop

```cpp

int detectAndRemoveLoop(node *head) {
    node *slow_ptr = head, *fast_ptr = head->next;
    while(fast_ptr != NULL && fast_ptr->next != NULL) {
        if(slow_ptr == fast_ptr)
            break;
        slow_ptr = slow_ptr->next;
        fast_ptr = fast_ptr->next->next;
    }
    
    if(slow_ptr != fast_ptr) 
        return 0;

    slow_ptr = head;
    while(slow_ptr != fast_ptr->next) {
        slow_ptr = slow_ptr->next;
        fast_ptr = fast_ptr->next;
    }
    fast_ptr->next = NULL;
    return 1;
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
head->next->next->next = head->next;
int loop = detectAndRemoveLoop(head);
if(loop)
    cout<<"Loop detected and removed"<<endl;
else
    cout<<"Loop not detected"<<endl;
```

#### Output

```cpp
Loop detected and removed
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/detect-and-remove-loop.cpp)

### 34. Add Two Linked Lists

```cpp

typedef long long ll;

void putNumberIntoLinkedList(node **ptr, ll no) {
	while(no) {
		insertAtEnd(&(*ptr), no%10);
		no /= 10;
	}
}

ll getNumberFromLinkedList(node *ptr) {
	ll multiplier = 1, no = 0;
	while(ptr != NULL) {
		no += ptr->data * multiplier;
		multiplier *= 10;
		ptr = ptr->next;
	}
	return no;
}

node* addTwoLists(node *x, node *y) {
	ll x_no = 0, y_no = 0;
	
	x_no = getNumberFromLinkedList(x);
	y_no = getNumberFromLinkedList(y);
	
	node *ptr = NULL;
	putNumberIntoLinkedList(&ptr,x_no + y_no);
	return ptr;
}
```

#### Example

```cpp

ll m, n;
cout<<"Enter 1st number: ";
cin>>m;
cout<<"Enter 2nd number: ";
cin>>n;
node *m_ptr = NULL, *n_ptr = NULL;

putNumberIntoLinkedList(&m_ptr, m);
putNumberIntoLinkedList(&n_ptr, n);

cout<<"1st number: ";
printList(m_ptr);

cout<<"2nd number: ";
printList(n_ptr);

node *sum = addTwoLists(m_ptr, n_ptr);
cout<<"Sum of Linked Lists: ";
printList(sum);
```

#### Output

```cpp
Enter 1st number: 64957
Enter 2nd number: 48
1st number: 7 -> 5 -> 9 -> 4 -> 6 -> NULL
2nd number: 8 -> 4 -> NULL
Sum of Linked Lists: 5 -> 0 -> 0 -> 5 -> 6 -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/add-two-numbers-represented-by-linked-list.cpp)

### 35. Union & Intersection

```cpp

node* intersectionofLinkedLists(node *x, node *y) {
	node *head = NULL;
	unordered_set<char> seen;
	while(x != NULL) {
		seen.insert(x->data);
		x = x->next;
	}

	while(y != NULL) {
		if(seen.find(y->data) != seen.end())
			insertAtEnd(&head,y->data);
		y = y->next;
	}

	return head;
}

node* unionofLinkedLists(node *x, node *y) {
	node *head = NULL;
	unordered_set<char> seen;

	while(x != NULL) {
		seen.insert(x->data);
		insertAtEnd(&head,x->data);
		x = x->next;
	}

	while(y != NULL) {
		if(seen.find(y->data) == seen.end())
			insertAtEnd(&head,y->data);
		y = y->next;
	}

	return head;
}
```

#### Example

```cpp

node *x = NULL;
insertAtEnd(&x, 'B');
insertAtEnd(&x, 'C');
insertAtEnd(&x, 'A');
insertAtEnd(&x, 'D');
insertAtEnd(&x, 'E');
printList(x);

node *y = NULL;
insertAtEnd(&y, 'F');
insertAtEnd(&y, 'C');
insertAtEnd(&y, 'G');
insertAtEnd(&y, 'D');
insertAtEnd(&y, 'H');
printList(y);

cout<<"Intersection: "<<endl;
printList(intersectionofLinkedLists(x,y));

cout<<"Union: "<<endl;
printList(unionofLinkedLists(x,y));
```

#### Output

```cpp
B -> C -> A -> D -> E -> NULL
F -> C -> G -> D -> H -> NULL
Intersection: 
C -> D -> NULL
Union: 
B -> C -> A -> D -> E -> F -> G -> H -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/union-and-intersection-of-linked-lists.cpp)

### 36. Triplet from 3 lists with sum equal to given no.

```cpp

bool triplet(node *x, node *yTemp, node *zTemp, dataType no) {
	mergeSort(&yTemp);
	mergeSort(&zTemp);
	iterativeReverse(&zTemp);

	while(x != NULL) {
		node *y = yTemp, *z = zTemp;
		while(y != NULL && z != NULL) {
			dataType sum = x->data + y->data + z->data;
			if(sum == no) {
				cout<<"Triplet Found : "<<x->data<<", "<<y->data<<", "<<z->data<<endl;
				return true;
			}
			else if(sum < no)
						y = y->next;
					else z = z->next;
		}
		x = x->next;
	}
	cout<<"No Triplet Found"<<endl;
	return false;
}
```

#### Example

```cpp

node *x = NULL;
insertAtEnd(&x, 14);
insertAtEnd(&x, 21);
insertAtEnd(&x, 32);
insertAtEnd(&x, 61);
insertAtEnd(&x, 71);
printList(x);

node *y = NULL;
insertAtEnd(&y, 11);
insertAtEnd(&y, 92);
insertAtEnd(&y, 23);
insertAtEnd(&y, 86);
insertAtEnd(&y, 107);
printList(y);

node *z = NULL;
insertAtEnd(&z, 321);
insertAtEnd(&z, 212);
insertAtEnd(&z, 32);
insertAtEnd(&z, 65);
insertAtEnd(&z, 77);
printList(z);

triplet(x,y,z,296);
```

#### Output

```cpp
14 -> 21 -> 32 -> 61 -> 71 -> NULL
11 -> 92 -> 23 -> 86 -> 107 -> NULL
321 -> 212 -> 32 -> 65 -> 77 -> NULL
Triplet Found : 61, 23, 212
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/find-triplet-from-3-linked-lists-with-sum-equal-to-given-no.cpp)

### 37. Rotate List `n` times Counter Clockwise

```cpp

void rotate(node **head, int n) {
	node *temp = *head;
	
	while(temp->next != NULL)
		temp = temp->next;

	temp->next = *head;

	temp = *head;
	while(--n)
		temp = temp->next;
	*head = temp->next;
	temp->next = NULL;
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'F');
insertAtStart(&head, 'E');
insertAtStart(&head, 'D');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
rotate(&head,4);
printList(head);
```

#### Output

```cpp
A -> B -> C -> D -> E -> F -> NULL
E -> F -> A -> B -> C -> D -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/rotate-a-linked-list.cpp)

### 38. Sort Lists of 0s, 1s & 2s

```cpp

typedef int dataType;

void sort(node *head) {
	node *temp = head;
	int count[3] = {0,0,0};
	
	while(temp != NULL) {
		count[temp->data]++;
		temp = temp->next;
	}

	temp = head;
	while(temp != NULL) {
		if(count[0]) {
			temp->data = 0;
			count[0]--;
		}
		else 
			if(count[1]) {
				temp->data = 1;
				count[1]--;
			}
			else temp->data = 2;
		temp = temp->next;	
	}
}
```

#### Example

```cpp

node *head = NULL;
insertAtEnd(&head, 0);
insertAtEnd(&head, 1);
insertAtEnd(&head, 2);
insertAtEnd(&head, 1);
insertAtEnd(&head, 0);
insertAtEnd(&head, 2);
insertAtEnd(&head, 2);
insertAtEnd(&head, 2);
insertAtEnd(&head, 0);
insertAtEnd(&head, 1);
insertAtEnd(&head, 2);
insertAtEnd(&head, 1);
printList(head);
sort(head);
printList(head);
```

#### Output

```cpp
0 -> 1 -> 2 -> 1 -> 0 -> 2 -> 2 -> 2 -> 0 -> 1 -> 2 -> 1 -> NULL
0 -> 0 -> 0 -> 1 -> 1 -> 1 -> 1 -> 2 -> 2 -> 2 -> 2 -> 2 -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/sort-linked-list-of-0s-1s-2s.cpp)

### 39. Skip `M` nodes Delete `N` nodes

```cpp

typedef int dataType;

void skipMDeleteN(node *head, int M, int N) {
	node *temp = head;
	while(temp != NULL) {

		for(int i = 0; i < M-1; i++)
			temp = temp->next;

		node *prev_ptr = temp;
		temp = temp->next;

		for(int i = 0; i < N; i++) {
			node *next_ptr = temp->next;
			free(temp);
			temp = next_ptr;
		}

		prev_ptr->next = temp;
	}
}
```

#### Example

```cpp

node *head = NULL;
insertAtEnd(&head, 1);
insertAtEnd(&head, 2);
insertAtEnd(&head, 3);
insertAtEnd(&head, 4);
insertAtEnd(&head, 5);
insertAtEnd(&head, 6);
insertAtEnd(&head, 7);
insertAtEnd(&head, 8);
insertAtEnd(&head, 9);
insertAtEnd(&head, 10);
printList(head);
skipMDeleteN(head,3,2);
printList(head);
```

#### Output

```cpp
1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10 -> NULL
1 -> 2 -> 3 -> 6 -> 7 -> 8 -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/skip-m-delete-n.cpp)

### 40. Merge a linked list into another linked list at alternate positions

```cpp

void mergeAtAlternatePostions(node *a, node **b) {
	node *p = a, *q = *b;

	while(p != NULL && q != NULL) {
		node *p_next = p->next;
		node *q_next = q->next;

		p->next = q;
		q->next = p_next;

		p = p_next;
		q = q_next;
	}

	*b = q;
}
```

#### Example

```cpp

node *a = NULL;
insertAtStart(&a, 'C');
insertAtStart(&a, 'B');
insertAtStart(&a, 'A');
cout<<"Linked List 1 : "<<endl;
printList(a);

node *b = NULL;
insertAtStart(&b, 'H');
insertAtStart(&b, 'G');
insertAtStart(&b, 'F');
insertAtStart(&b, 'E');
insertAtStart(&b, 'D');
cout<<"Linked List 2 : "<<endl;
printList(b);

mergeAtAlternatePostions(a,&b);
cout<<"Modified Linked List 1 : "<<endl;
printList(a);
cout<<"Modified Linked List 2 : "<<endl;
printList(b);
```

#### Output

```cpp
Linked List 1 : 
A -> B -> C -> NULL
Linked List 2 : 
D -> E -> F -> G -> H -> NULL
Modified Linked List 1 : 
A -> D -> B -> E -> C -> F -> NULL
Modified Linked List 2 : 
G -> H -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/merge-a-linked-list-into-another-at-alternate-positions.cpp)

### 41. Pairwise swap elements of a given linked list by changing links

```cpp

void pairWiseSwap(node **head) {
	
	if(*head == NULL || (*head)->next == NULL)
		return;
		
	node *prev = *head, *curr = prev->next;
	*head = curr;
	
	while(true) {
		node *next_ptr = curr->next;
		curr->next = prev;

		if(next_ptr == NULL || next_ptr->next == NULL) {
			prev->next = next_ptr;
			break;
		}

		prev->next = next_ptr->next;

		prev = next_ptr;
		curr = prev->next;
	}
}
```

#### Example

```cpp

node *head = NULL;
insertAtStart(&head, 'F');
insertAtStart(&head, 'E');
insertAtStart(&head, 'C');
insertAtStart(&head, 'B');
insertAtStart(&head, 'A');
printList(head);
pairWiseSwap(&head);
printList(head);
```

#### Output

```cpp
A -> B -> C -> E -> F -> NULL
B -> A -> E -> C -> F -> NULL
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/pairwise-swap-elements-of-linked-list-by-changing-links.cpp)

## Array

Array is a data structure used to store homogeneous elements at contiguous locations. Size of an array must be provided before storing data.

#### General Tip

<p class="tip">~x = x + 1</p>

<p class="warning">~~x = x </p>
 
### 1. Print

```cpp

void printArray(int arr[], int len) {
	cout<<"The given array is : {";
	for (int i = 0; i < len; ++i)
		cout<<" "<<arr[i];
	cout<<" }"<<endl;
}
```

### 2. Search in an Unsorted array

<p class="danger">In C / C++, if array value is not inserted, then it returns Garbage Value</p>


```cpp

int searchUnsorted(int arr[], int len, int value) {
	for(int i = 0; i < len; i++)
		if(arr[i] == value)
			return i;
	return -1;
}
```

#### Example

```cpp

int arr[10] = {278,12,356,420};
int len = sizeof(arr) / sizeof(arr[0]);
printArray(arr,4);
int pos = searchUnsorted(arr, len,52);
if(!~pos)
	cout<<"Element 52 not found"<<endl;
else cout<<"Element 52 found at position "<<(pos + 1)<<endl;
```

#### Output

```cpp
The given array is : { 278 12 356 420 }
Element 52 not found

```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/search-in-an-unsorted-array.cpp)

### 3. Insert in an Unsorted array

```cpp

int insertUnsorted(int arr[], int len, int n, int value) {
	if(n >= len)
		return n;
	arr[n] = value;
	return n + 1;
}
```

#### Example

```cpp

int arr[10] = {278,12,356,420};
int len = sizeof(arr) / sizeof(arr[0]);
printArray(arr,4);
int newLen = insertUnsorted(arr, len,4,977);
if(newLen == len)
	cout<<"Cannot insert as array is completely filled"<<endl;
else 	
	cout<<"Element 977 inserted at position "<<newLen<<" successfully"<<endl;
printArray(arr,5);
```

#### Output

```cpp
The given array is : { 278 12 356 420 }
Element 977 inserted at position 5 successfully
The given array is : { 278 12 356 420 977 }
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/insert-in-an-unsorted-array.cpp)

### 4. Delete in an Unsorted array

```cpp

int deleteUnsorted(int arr[], int len, int value) {
	int pos = searchUnsorted(arr,len,value);
	if(pos == -1)
		return len;
	while(pos < len) {
		arr[pos] = arr[pos+1];
		pos++;
	}
	return len-1;
}
```

#### Example

```cpp

int arr[10] = {278,12,356,420};
int len = sizeof(arr) / sizeof(arr[0]);
printArray(arr,4);
int newLen = deleteUnsorted(arr, len,12);
if(newLen == len)	
	cout<<"Element 12 not found"<<endl;
else cout<<"Element 12 deleted successfully"<<endl;
printArray(arr,3);
```

#### Output

```cpp
The given array is : { 278 12 356 420 }
Element 12 deleted successfully
The given array is : { 278 356 420 }
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/delete-in-an-unsorted-array.cpp)

### 5. Search in a Sorted array

<p class="tip">Sorting with Binary Search is faster than sorting iteratively</p>

```cpp

int binarySearch(int arr[], int low, int high, int value) {
	if(high < low) 
		return -1;
	int mid = (low + high) / 2;
	if(arr[mid] == value)
		return mid;
	if(value < arr[mid])
		return binarySearch(arr,low, mid - 1, value);
	return binarySearch(arr,mid + 1, high, value);
}
```

#### Example

```cpp

int arr[10] = {12,278,356,420};
int len = sizeof(arr) / sizeof(arr[0]);
printArray(arr,4);
int search = binarySearch(arr,0,3,356);	
if(!~search)
	cout<<"Element 356 not found"<<endl;
else cout<<"Element 356 found at positon "<<(search + 1)<<endl;
```

#### Output

```cpp
The given array is : { 12 278 356 420 }
Element 356 found at positon 3
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/search-in-a-sorted-array.cpp)

### 3. Insert in a Sorted array

```cpp

int insertSorted(int arr[], int len, int value) {
	int i;
	for(i = len - 1; i >= 0 && arr[i] > value; i--)
		arr[i+1] = arr[i];
	arr[i+1] = value;
	cout<<"Element "<<value<<" inserted at position "<<(i+2)<<" successfully"<<endl;
	return len + 1;
}
```

#### Example

```cpp

int arr[10] = {12,278,356,420};
int len = 4;
printArray(arr,len);
len = insertSorted(arr,len,4);
printArray(arr,len);
```

#### Output

```cpp
The given array is : { 12 278 356 420 }
Element 4 inserted at position 1 successfully
The given array is : { 4 12 278 356 420 }
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/insert-in-a-sorted-array.cpp)

### 4. Delete in a Sorted array

```cpp

int deleteSorted(int arr[], int len, int value) {
	int pos = binarySearch(arr,0,len-1,value);
	if(!~pos)
		return len;
	while(pos < len) {
		arr[pos] = arr[pos+1];
		pos++;
	}
	return len - 1;
}
```

#### Example

```cpp

int arr[10] = {12,278,356,420};
int len = 4;
printArray(arr,len);
int newLen = deleteSorted(arr, len,12);
if(newLen == len)
	cout<<"Element 12 not found"<<endl;
else cout<<"Element 12 deleted successfully"<<endl;
printArray(arr,newLen);
```

#### Output

```cpp
The given array is : { 12 278 356 420 }
Element 12 deleted successfully
The given array is : { 278 356 420 }
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/delete-in-a-sorted-array.cpp)

### 5. Check if a pair in array equals a value

#### A. Sorting

```cpp

void hasArrayTwoCandidatesUsingSorting(int arr[],int len, int sum) {
	int i = 0, j = len - 1;
	while(i < j)
		if(arr[i] + arr[j] == sum)
			break;
		else 
			if(arr[i] + arr[j] < sum)
				i++;
			else j--;
	if(i < j)
		cout<<"Pairs "<<arr[i]<<" and "<<arr[j]<<" equals to "<<sum<<endl;
	else cout<<"No Candidates Found"<<endl;
}
```

#### B. Hash Map

```cpp

void hasArrayTwoCandidatesUsingHashMap(int arr[], int len, int sum) {
	unordered_set<int> seen;
	for(int i = 0; i < len; i++)
		if(seen.find(arr[i]) == seen.end())
			seen.insert(sum-arr[i]);
		else {
			cout<<"Pairs "<<arr[i]<<" and "<<sum-arr[i]<<" equals to "<<sum<<endl;
			return;
		}
	cout<<"No Candidates Found"<<endl;	
}
```

#### Example

```cpp

int arr[5] = {4,2,3,1,5};
printArray(arr,5);
sort(arr,arr+5);
hasArrayTwoCandidatesUsingSorting(arr,5,6);
int arr1[5] = {4,2,3,1,5};
printArray(arr1,5);
hasArrayTwoCandidatesUsingHashMap(arr1,5,6);
```

#### Output

```cpp
The given array is : { 4 2 3 1 5 }
Pairs 1 and 5 equals to 6
The given array is : { 4 2 3 1 5 }
Pairs 2 and 4 equals to 6
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/check-if-sum-of-pair-in-array-equals-to-value.cpp)

### 6. Majority Element

<p class="tip">A majority element in an array A[] of size n is an element that appears more than n/2 times</p>

#### A. Map

```cpp

int majorityElementUsingMap(int arr[], int len) {
	map<int,int> freq;
	for(int i = 0; i < len; i++)
		if(!freq[arr[i]])
			freq[arr[i]] = 1;
		else freq[arr[i]]++;
	for(int i = 0; i < len; i++)
		if(freq[arr[i]] > len/2)
			return arr[i];
	return 0;
}

void printMajorityUsingMap(int arr[], int len) {
	int cand = majorityElementUsingMap(arr,9);
	if(cand)
		cout<<"Majority Element Using Map  : "<<cand<<endl;
	else cout<<"No Majority Element Using Map"<<endl;	
}
```

#### B. Moore's Voting Algorithm

```cpp

int findCandidate(int arr[], int len) {
	int major_i = 0, count = 1;
	for(int i = 1; i < len; i++) {
		if(arr[major_i] == arr[i])
			count++;
		else count--;
		if(count == 0) {
			major_i = i;
			count = 1;
		}
	}
	return arr[major_i];
}

bool isMajor(int arr[], int len, int cand) {
	int count = 0;
	for(int i = 0; i < len; i++)
		if(arr[i] == cand)
			count++;
	if(count > len/2)
		return 1;
	return 0;	
}

void printMajorityUsingMoore(int arr[], int len) {
	int cand = findCandidate(arr,len);
	if(cand)
		cout<<"Majority Element Using Moore's Voting Algorithm  : "<<cand<<endl;
	else cout<<"No Majority Element Using Moore's Voting Algorithm"<<endl;
}
```

#### Example

```cpp

int arr[9] = {3,3,4,2,4,4,2,4,4};
printArray(arr,9);
printMajorityUsingMap(arr,9);
printMajorityUsingMoore(arr,9);
```

#### Output

```cpp
The given array is : { 3 3 4 2 4 4 2 4 4 }
Majority Element Using Map  : 4
Majority Element Using Moore's Voting Algorithm  : 4
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/majority-element.cpp)

### 7. Find Number occuring Odd no. of times

```cpp

int getOccurrences(int arr[], int len) {
	int num = arr[0];
	for(int i = 1; i < len; ++i)
		num ^= arr[i];
	return num;
}
```

#### Example

```cpp

int arr[] = {2, 3, 5, 4, 5, 2, 4, 3, 5, 2, 4, 4, 2};
int len = sizeof(arr) / sizeof(arr[0]);
printArray(arr,len);
cout<<"Number: "<<getOccurrences(arr, len);
```

#### Output

```cpp

The given array is : { 2 3 5 4 5 2 4 3 5 2 4 4 2 }
Number: 5
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/find-no-occuring-odd-number-of-times.cpp)

### 8. Largest Sum Contiguous Array

#### A. Kadane's Algorithm

<p class="warning">Does not work for Negative Numbers</p>

```cpp

int largestSubArraySumKadane(int arr[], int len, int *start, int *end) {
	int max_so_far = 0, max_ending_here = 0, s = 0;
	for(int i = 0; i < len; ++i) {
		max_ending_here += arr[i];
		if(max_ending_here < 0) {
			max_ending_here = 0;
			s = i + 1;
		}
		else
			if(max_so_far < max_ending_here) {
				max_so_far = max_ending_here;
				*start = s;
				*end = i;
			}
	}
	return max_so_far;
}
```

#### B. Dynamic Programming

```cpp

int largestSubArraySumDP(int arr[], int len) {
	int curr_max = arr[0], max_so_far = arr[0];
	for(int i = 1; i < len; i++) {
		curr_max = max(arr[i], curr_max + arr[i]);
		max_so_far = max(max_so_far, curr_max);
	}
	return max_so_far;
}
```

#### Example

```cpp

int arr[] = {-2, -3, 4, -1, -2, 1, 5, -3};
int len = sizeof(arr) / sizeof(arr[0]);
printArray(arr,len);
int start = 0, end = 0;
cout<<"Largest SubArray Sum using Kadane's: "<<largestSubArraySumKadane(arr, len, &start, &end)<<",Start Index: "<<start<<",End Index: "<<end<<endl;
cout<<"Largest SubArray Sum using Dynamic Programming: "<<largestSubArraySumDP(arr, len)<<endl;
```

#### Output

```cpp

The given array is : { -2 -3 4 -1 -2 1 5 -3 }
Largest SubArray Sum using Kadane's: 7,Start Index: 0,End Index: 0
Largest SubArray Sum using Dynamic Programming: 7
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/largest-sum-contiguous-array.cpp)

### 9. Find the Missing Number

#### A. Using Sum

```cpp

int missingNoUsingSum(int arr[], int n) {
	int sum = 0;
	int total = n*(n+1)/2;
	for(int i = 0; i < n; i++)
		sum += arr[i];
	return total - sum;
}
```

#### B. XOR

```cpp

int missingNoUsingXOR(int arr[], int n) {
	int xor1 = arr[0];
	for (int i = 1; i < n; ++i)
		xor1 ^= arr[i];
	int xor2 = 1;
	for (int i = 2; i <= n; ++i)
		xor2 ^= i;
	return xor1 ^ xor2;
}
```

#### Example

```cpp

int arr[] = {1,2,4,5,6};
printArray(arr,5);
cout<<"Missing Number Using Sum: "<<missingNoUsingSum(arr,6)<<endl;
cout<<"Missing Number Using XOR: "<<missingNoUsingXOR(arr,6)<<endl;
```

#### Output

```cpp

The given array is : { 1 2 4 5 6 }
Missing Number Using Sum: 3
Missing Number Using XOR: 3
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/find-the-missing-no.cpp)

### 10. Search an element in a sorted and rotated array

```cpp

int search(int arr[], int low, int high, int no) {
	if(low > high) return -1;

	int mid = (low+high)/2;
	if(no == arr[mid]) return mid;
	if(arr[low] <= arr[mid]) {
		if(no >= arr[low] && no <= arr[mid])
			return search(arr,low,mid-1,no);
		return search(arr,mid+1,high,no);
	}
	if(no >= arr[mid] && no <= arr[high])
		return search(arr,mid+1,high,no);
	return search(arr,low,mid-1,no);
}
```

#### Example

```cpp

int arr[] = {5, 6, 7, 8, 9, 10, 1, 2, 3};
int len = sizeof(arr)/sizeof(arr[0]);
printArray(arr,len);
int index = search(arr,0,len-1,3);
if(!~index)
	cout<<"Element not found"<<endl;
else cout<<"Index: "<<index<<endl;
```

#### Output

```cpp

The given array is : { 5 6 7 8 9 10 1 2 3 }
Index: 8
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/search-an-element-in-sorted-and-rotated-array.cpp)

### 11. Merge 2 Arrays

```cpp

int *merge(int x[], int y[], int m, int n) {
	int *arr=new int[m+n], i=0, j=0, k=0;
	while(i<m && j<n)
		if(x[i] <= y[j])
			arr[k++] = x[i++];
		else arr[k++] = y[j++];
	while(i<m)
		arr[k++] = x[i++];
	while(j<n)
		arr[k++] = y[j++];
	return arr;
}
```

#### Example

```cpp

int x[] = {2,7,10};
int y[] = {5,8,12,14};
int m = sizeof(x)/sizeof(x[0]);
int n = sizeof(y)/sizeof(y[0]);
cout<<"Displaying x "<<endl;
printArray(x,m);
cout<<"Displaying y "<<endl;
printArray(y,n);
cout<<"Displaying Merged Array "<<endl;
printArray(merge(x,y,m,n),m+n);
```

#### Output

```cpp

Displaying x 
The given array is : { 2 7 10 }
Displaying y 
The given array is : { 5 8 12 14 }
Displaying Merged Array 
The given array is : { 2 5 7 8 10 12 14 }
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/merge-2-arrays.cpp)

### 12. Reverse an Array

#### A. Iterative

```cpp

void reverseIterative(int arr[], int len) {
	for(int start = 0, end = len-1; start < end; ++start, --end)
		swap(&arr[start],&arr[end]);
}
```

#### B. Recursive

```cpp

void reverseRecursive(int arr[], int start, int end) {
	if(start >= end) return;

	swap(&arr[start],&arr[end]);
	return reverseRecursive(arr,start+1,end-1);
}
```

#### Example

```cpp

int arr[] = {5, 6, 7, 8, 9, 10, 1, 2, 3};
int len = sizeof(arr)/sizeof(arr[0]);
printArray(arr,len);
reverseIterative(arr,len);
printArray(arr,len);
reverseRecursive(arr,0,len-1);
printArray(arr,len);
```

#### Output

```cpp

The given array is : { 5 6 7 8 9 10 1 2 3 }
The given array is : { 3 2 1 10 9 8 7 6 5 }
The given array is : { 5 6 7 8 9 10 1 2 3 }
```

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/array/reverse-an-array.cpp)