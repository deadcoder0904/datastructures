# Data Structures in C++

Same Old Shite :joy: written, edited & verified by [A2K](https://github.com/deadcoder0904)

## Linked List

```cpp
typedef struct node {
	int data;
	struct node *next;
} node;
```

### Insertion

Insertion in a linked list can be done in 3 ways - 

<p class="warning">(1) Insert at First</p>

![linked-list-insertion-1](assets/img/linked-list-insertion-1.png)

```cpp
void insertAtFirst(node **head, int data) {
	node* new_node = (node*) malloc(sizeof(node));
	new_node -> data = data;
	new_node -> next = *head;
	*head = new_node;
}
```

<p class="tip">(2) Insert after a Node</p>

![linked-list-insertion-2](assets/img/linked-list-insertion-2.png)

```cpp

```

<p class="danger">(3) Insert in the end</p>

![linked-list-insertion-3](assets/img/linked-list-insertion-3.png)

```cpp

```
