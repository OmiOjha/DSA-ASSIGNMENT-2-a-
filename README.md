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
