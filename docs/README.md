# Data Structures in C++

Same Old Shite :joy: written, compiled & coded by [A2K](https://github.com/deadcoder0904)

## Linked List

### Structure

```cpp

typedef char dataType;

typedef struct node {
	dataType data;
	struct node *next;
} node;

```

### Printing

```cpp

void printList(node *node) {
	while(node != NULL) {
		cout<<(node->data)<<" -> ";
		node = node->next;
	}
	cout<<"NULL";
}

```

### Insertion

Insertion in a linked list can be done in 3 ways - 

#### 1. Insert at Start

![linked-list-insertion-1](assets/img/linked-list-insertion-1.png)

```cpp

void insertAtStart(node **head, dataType data) {
	node* new_node = (node*) malloc(sizeof(node));
	
	new_node->data = data;
	new_node->next = *head;
	
	*head = new_node;
}

```

#### 2. Insert after a Node

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

#### 3. Insert in the end

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

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/insert.cpp)

### Deletion

#### 1. Deleting a given key

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

#### 2. Deleting a key at given position

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
