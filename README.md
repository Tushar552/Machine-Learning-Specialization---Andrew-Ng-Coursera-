### 1. Linear Search and Binary Search

#### Linear Search:
```c
#include <stdio.h>

int linearSearch(int arr[], int size, int key) {
    for(int i = 0; i < size; i++) {
        if(arr[i] == key) {
            return i;
        }
    }
    return -1;
}

int main() {
    int arr[] = {3, 6, 2, 8, 4, 1};
    int key = 8;
    int size = sizeof(arr)/sizeof(arr[0]);
    
    int result = linearSearch(arr, size, key);
    if(result != -1) {
        printf("Element found at index %d\n", result);
    } else {
        printf("Element not found\n");
    }
    
    return 0;
}
```

#### Binary Search:
```c
#include <stdio.h>

int binarySearch(int arr[], int size, int key) {
    int low = 0, high = size - 1;
    
    while(low <= high) {
        int mid = low + (high - low) / 2;
        
        if(arr[mid] == key) {
            return mid;
        }
        if(arr[mid] < key) {
            low = mid + 1;
        } else {
            high = mid - 1;
        }
    }
    return -1;
}

int main() {
    int arr[] = {1, 2, 3, 4, 6, 8};
    int key = 6;
    int size = sizeof(arr)/sizeof(arr[0]);
    
    int result = binarySearch(arr, size, key);
    if(result != -1) {
        printf("Element found at index %d\n", result);
    } else {
        printf("Element not found\n");
    }
    
    return 0;
}
```

### 2. Bubble Sort and Selection Sort

#### Bubble Sort:
```c
#include <stdio.h>

void bubbleSort(int arr[], int size) {
    for(int i = 0; i < size-1; i++) {
        for(int j = 0; j < size-i-1; j++) {
            if(arr[j] > arr[j+1]) {
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}

int main() {
    int arr[] = {64, 25, 12, 22, 11};
    int size = sizeof(arr)/sizeof(arr[0]);
    
    bubbleSort(arr, size);
    
    printf("Sorted array: ");
    for(int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    return 0;
}
```

#### Selection Sort:
```c
#include <stdio.h>

void selectionSort(int arr[], int size) {
    for(int i = 0; i < size-1; i++) {
        int min_idx = i;
        for(int j = i+1; j < size; j++) {
            if(arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }
        int temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
    }
}

int main() {
    int arr[] = {64, 25, 12, 22, 11};
    int size = sizeof(arr)/sizeof(arr[0]);
    
    selectionSort(arr, size);
    
    printf("Sorted array: ");
    for(int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    return 0;
}
```

### 3. Merge Sort and Quick Sort

#### Merge Sort:
```c
#include <stdio.h>

void merge(int arr[], int l, int m, int r) {
    int n1 = m - l + 1;
    int n2 = r - m;
    int L[n1], R[n2];
    
    for(int i = 0; i < n1; i++) L[i] = arr[l + i];
    for(int i = 0; i < n2; i++) R[i] = arr[m + 1 + i];
    
    int i = 0, j = 0, k = l;
    while(i < n1 && j < n2) {
        if(L[i] <= R[j]) {
            arr[k++] = L[i++];
        } else {
            arr[k++] = R[j++];
        }
    }
    
    while(i < n1) arr[k++] = L[i++];
    while(j < n2) arr[k++] = R[j++];
}

void mergeSort(int arr[], int l, int r) {
    if(l < r) {
        int m = l + (r - l) / 2;
        mergeSort(arr, l, m);
        mergeSort(arr, m+1, r);
        merge(arr, l, m, r);
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6, 7};
    int size = sizeof(arr)/sizeof(arr[0]);
    
    mergeSort(arr, 0, size - 1);
    
    printf("Sorted array: ");
    for(int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    return 0;
}
```

#### Quick Sort:
```c
#include <stdio.h>

void swap(int* a, int* b) {
    int t = *a;
    *a = *b;
    *b = t;
}

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);
    
    for(int j = low; j <= high-1; j++) {
        if(arr[j] < pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if(low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main() {
    int arr[] = {10, 7, 8, 9, 1, 5};
    int size = sizeof(arr)/sizeof(arr[0]);
    
    quickSort(arr, 0, size - 1);
    
    printf("Sorted array: ");
    for(int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    
    return 0;
}
```

### 4. Stacks and Queues

#### Stack Implementation:
```c
#include <stdio.h>
#define MAX 100

int stack[MAX];
int top = -1;

void push(int x) {
    if(top == MAX - 1) {
        printf("Stack Overflow\n");
        return;
    }
    stack[++top] = x;
}

void pop() {
    if(top == -1) {
        printf("Stack Underflow\n");
        return;
    }
    printf("Popped element: %d\n", stack[top--]);
}

void display() {
    if(top == -1) {
        printf("Stack is empty\n");
        return;
    }
    for(int i = 0; i <= top; i++) {
        printf("%d ", stack[i]);
    }
    printf("\n");
}

int main() {
    push(10);
    push(20);
    push(30);
    
    display();
    
    pop();
    display();
    
    return 0;
}
```

#### Queue Implementation:
```c
#include <stdio.h>
#define MAX 100

int queue[MAX];
int front = -1, rear = -1;

void enqueue(int x) {
    if(rear == MAX - 1) {
        printf("Queue Overflow\n");
        return;
    }
    if(front == -1) front = 0;
    queue[++rear] = x;
}

void dequeue() {
    if(front == -1 || front > rear) {
        printf("Queue Underflow\n");
        return;
    }
    printf("Dequeued element: %d\n", queue[front++]);
}

void display() {
    if(front == -1 || front > rear) {
        printf("Queue is empty\n");
        return;
    }
    for(int i = front; i <= rear; i++) {
        printf("%d ", queue[i]);
    }
    printf("\n");
}

int main() {
    enqueue(10);
    enqueue(20);
    enqueue(30);
    
    display();
    
    dequeue();
    display();
    
    return 0;
}
```

### 5. Singly Linked List

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

void insertAtEnd(struct Node** head, int new_data) {
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));
    struct Node* last = *head;
    new_node->data = new_data;
    new_node->next = NULL;
    
    if(*head == NULL) {
        *head = new_node;
        return;
    }
    
    while(last->next

 != NULL) last = last->next;
    last->next = new_node;
}

void printList(struct Node* node) {
    while(node != NULL) {
        printf("%d ", node->data);
        node = node->next;
    }
    printf("\n");
}

int main() {
    struct Node* head = NULL;
    
    insertAtEnd(&head, 1);
    insertAtEnd(&head, 2);
    insertAtEnd(&head, 3);
    
    printList(head);
    
    return 0;
}
```

### 6. Doubly Linked List

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
    struct Node* prev;
};

void insertAtEnd(struct Node** head, int new_data) {
    struct Node* new_node = (struct Node*) malloc(sizeof(struct Node));
    struct Node* last = *head;
    new_node->data = new_data;
    new_node->next = NULL;
    
    if(*head == NULL) {
        new_node->prev = NULL;
        *head = new_node;
        return;
    }
    
    while(last->next != NULL) last = last->next;
    last->next = new_node;
    new_node->prev = last;
}

void printList(struct Node* node) {
    struct Node* last;
    printf("Traversal in forward direction: ");
    while(node != NULL) {
        printf("%d ", node->data);
        last = node;
        node = node->next;
    }
    printf("\n");
    
    printf("Traversal in reverse direction: ");
    while(last != NULL) {
        printf("%d ", last->data);
        last = last->prev;
    }
    printf("\n");
}

int main() {
    struct Node* head = NULL;
    
    insertAtEnd(&head, 1);
    insertAtEnd(&head, 2);
    insertAtEnd(&head, 3);
    
    printList(head);
    
    return 0;
}
```

### 7. Binary Search Tree

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Node* newNode(int data) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

struct Node* insert(struct Node* node, int data) {
    if(node == NULL) return newNode(data);
    if(data < node->data)
        node->left = insert(node->left, data);
    else if(data > node->data)
        node->right = insert(node->right, data);
    
    return node;
}

void inorder(struct Node* root) {
    if(root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

int main() {
    struct Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);
    
    inorder(root);
    
    return 0;
}
```

### 8. Tree Traversal Algorithms

#### Inorder, Preorder, and Postorder Traversal:

```c
#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Node* newNode(int data) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = data;
    node->left = node->right = NULL;
    return node;
}

void inorder(struct Node* root) {
    if(root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

void preorder(struct Node* root) {
    if(root != NULL) {
        printf("%d ", root->data);
        preorder(root->left);
        preorder(root->right);
    }
}

void postorder(struct Node* root) {
    if(root != NULL) {
        postorder(root->left);
        postorder(root->right);
        printf("%d ", root->data);
    }
}

int main() {
    struct Node* root = newNode(1);
    root->left = newNode(2);
    root->right = newNode(3);
    root->left->left = newNode(4);
    root->left->right = newNode(5);
    
    printf("Inorder traversal: ");
    inorder(root);
    printf("\n");
    
    printf("Preorder traversal: ");
    preorder(root);
    printf("\n");
    
    printf("Postorder traversal: ");
    postorder(root);
    printf("\n");
    
    return 0;
}
```
