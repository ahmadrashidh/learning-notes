# Linked List

## Limitations of Arrays
- Arrays are contiguously stored
- Allows random access with time complexity O(1)

| Operation/Time complexity | At start | At end | At k-th position |
|---------------------------|----------|--------|------------------|
| Insertion                 | O(N)     | O(1)   | O(N)             |
| Deletion                  | O(N)     | O(1)   | O(N)             |

## Implementation of LinkedList

### Linkedlist Node Object

```java
class Node {
    int value; // can be any datatype
    Node next;

    Node(int value){
        this.value = value;
        this.next = null;
    }
}


Node a = new Node(12); // [12]->null
a.next = new Node(15); // [12]->[15]->null
a.next.next = new Node(20); // [12]->[15]->[20]->null

```
### Insertion at start

```java

Node insertAtStart(Node head, int value){
    // head is null if is linked list is empty.
    Node newNode = new Node(value); 
    newNode.next = head; // [value]->[]:head
    head = node; // head:[value]->
    return head;
}

```
### Insertion at end

```java

Node insertAtEnd(Node head, int value){

    Node newNode = new Node(value);
    if(head == null){
        head = newNode;
    } else {
        Node curr = head;
        while(curr.next != null){
            curr = curr.next;
        }
        curr.next = newNode;
    }

    
    return head;
}


```

TC:O(N) -> O(1) using tail pointer

### Insert at Kth position

```java
Node insertAtKth(Node head, int value, int k){
    if(k == 0){

        insertAtStart(head, value);

    } else {

        Node newNode = new Node(value);

        int pos = 0;
        Node curr = head;
        while(pos < k){
            pos++;
            curr = curr.next;
        }
    
        newNode.next = curr.next;
        curr.next = newNode;

    }

    return head;
}
```
TC:O(N)











