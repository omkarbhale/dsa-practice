# Design Double-ended Queue (Deque)

Design a double-ended queue (deque) data structure that supports the following operations:
- `void insertFront(int value)`: Inserts an element at the front of the deque.
- `void insertLast(int value)`: Inserts an element at the back of the deque.
- `int deleteFront()`: Removes and returns the element at the front of the deque. If the deque is empty, return -1.
- `int deleteLast()`: Removes and returns the element at the back of the deque. If the deque is empty, return -1.
- `int getFront()`: Returns the element at the front of the deque without removing it. If the deque is empty, return -1.
- `int getRear()`: Returns the element at the back of the deque without removing it. If the deque is empty, return -1.
- `bool isEmpty()`: Returns true if the deque is empty, false otherwise.

## Solution

- Make sure all prev and next pointers are correct after each operation
- Remember to handle operations on empty deque

```java
class Deque {
    class DequeNode {
        int value;
        DequeNode next;
        DequeNode prev;
        DequeNode(int value) {
            this.value = value;
            next = null;
            prev = null;
        }
        @Override
        public String toString() {
            return "" + value;
        }
    }

    DequeNode head;
    DequeNode tail;
    public Deque() {
        head = null;
        tail = null;
    }

    void insertFront(int value) {
        // To Insert at head, we make new head
        DequeNode node = new DequeNode(value);
        if (head == null) {
            tail = node;    
        } else {
            head.prev = node;
            node.next = head;
        }
        head = node;
    }

    void insertLast(int value) {
        // To insert at last, we make new tail
        DequeNode node = new DequeNode(value);
        if (head == null) {
            head = node;
        } else {
            tail.next = node;
            node.prev = tail;
        }
        tail = node;
    }

    int popFront() {
        if (head == null) {
            return -1;
        }

        int value = head.value;
        head.next.prev = null;
        head = head.next;
        return value;
    }

    int popBack() {
        if (tail == null) {
            return -1;
        }

        int value = tail.value;
        tail.prev.next = null;
        tail = tail.prev;
        return value;
    }

    int front() {
        return head == null ? -1 : head.value;
    }

    int back() {
        return tail == null ? -1 : tail.value;
    }

    boolean isEmpty() {
        return head == null;
    }

    @Override
    public String toString() {
        DequeNode curr = head;
        StringBuilder sb = new StringBuilder();
        while (curr != null) {
            sb.append("[");
            sb.append("prev:" + curr.prev + ",");
            sb.append("this:" + curr.value + ",");
            sb.append("next:" + curr.next);
            sb.append("]");
            sb.append(" => ");
            curr = curr.next;
        }
        return sb.toString();
    }
}
```
<details> <summary>Tests</summary>

```java
class Solution {
    public static void main(String[] args) {
        testDequeOperations();
        System.out.println("Tests complete!");
    }

    public static void testDequeOperations() {
        Deque deque = new Deque();

        // Test insertFront and front
        deque.insertFront(1);
        assert deque.front() == 1;
        deque.insertFront(2);
        assert deque.front() == 2;

        // Test insertLast and back
        deque.insertLast(3);
        assert deque.back() == 3;
        deque.insertLast(4);
        assert deque.back() == 4;

        System.out.println(deque);

        // Test popFront
        assert deque.popFront() == 2;
        assert deque.popFront() == 1;
        assert deque.popFront() == 3;

        // Test popBack
        assert deque.popBack() == 4;
        assert deque.popBack() == -1; // Deque is empty now

        // Test isEmpty
        assert deque.isEmpty();
    }
}
```

</details>