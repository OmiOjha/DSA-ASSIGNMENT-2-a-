//linked list structure in c

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

// Function to create a new node
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}

//Inserting a Node in the Middle

void insertMiddle(struct Node** head, int data) {
   
    struct Node* newNode = createNode(data);
    
    if (*head == NULL) { // If the list is empty
        *head = newNode;
        return;
    }

    struct Node* slow = *head;
    struct Node* fast = *head;

    // Find the middle using slow and fast pointers
    while (fast->next != NULL && fast->next->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }

    // Insert the new node after the middle node (pointed by slow)
    newNode->next = slow->next;
    slow->next = newNode;
}
// Deleting the Middle Node
void deleteMiddle(struct Node** head) {
    if (*head == NULL || (*head)->next == NULL) {
        // If the list is empty or has only one element, set head to NULL
        free(*head);
        *head = NULL;
        return;
    }

    struct Node* slow = *head;
    struct Node* fast = *head;
    struct Node* prev = NULL;

    // Find the middle node and its previous node
    while (fast != NULL && fast->next != NULL) {
        fast = fast->next->next;
        prev = slow;
        slow = slow->next;
    }

    // Delete the middle node by skipping it in the list
    prev->next = slow->next;
    free(slow);
}
// Helper function to test insertion and deletion
void printList(struct Node* head) {
    struct Node* current = head;
    while (current != NULL) {
        printf("%d -> ", current->data);
        current = current->next;
    }
    printf("NULL\n");
}

int main() {
    // Creating a sample linked list: 1 -> 2 -> 3 -> 4 -> 5
    
    struct Node* head = createNode(1);
    
    head->next = createNode(2);
    head->next->next = createNode(3);
    head->next->next->next = createNode(4);
    head->next->next->next->next = createNode(5);

    printf("Original List:\n");
    printList(head);

    // Insert in the middle
    insertMiddle(&head, 99);
    printf("After Inserting 99 in the middle:\n");
    printList(head);

    // Delete the middle node
    deleteMiddle(&head);
    printf("After Deleting the middle node:\n");
    printList(head);

    return 0;
}
