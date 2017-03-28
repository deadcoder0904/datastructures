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

#### Deleting a Node

![linked-list-deleting-a-node](./assets/img/linked-list-deleting-a-node.png)

```cpp

void deleteNode(node **head, dataType key) {
	node *temp = *head, *prev;
	if(temp != NULL && temp->data == key) {
		cout<<"List is empty"<<endl;
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

#### Example

```cpp

	node *head = NULL;
	insertAtStart(&head, 'C');
	insertAtStart(&head, 'B');
	insertAtStart(&head, 'A');
	deleteNode(&head, 'B');
	printList(head);

```

#### Output

<p class="tip">A -> C -> NULL</p>

#### [Complete Program](https://github.com/deadcoder0904/datastructures-practice/blob/master/linked-list/delete-a-node.cpp)
