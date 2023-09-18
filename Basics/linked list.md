# Design Singly Linked List
Design a Singly Linked List class.

Your `LinkedList` class should support the following operations:
- `LinkedList()` will initialize an empty linked list.
- `int get(int i)` will return the value of the ith node (0-indexed). If the index is out of bounds, return -1.
- `void insertHead(int val)` will insert a node with val at the head of the list.
- `void insertTail(int val)` will insert a node with val at the tail of the list.
- `int remove(int i)` will remove the ith node (0-indexed). If the index is out of bounds, return false, otherwise return true.
- `int[] getValues()` return an array of all the values in the linked list, ordered from head to tail.

## Solution

Just make sure to remember to handle edge cases in all cases, such as
- If `head` does not exist yet for each operation
- There is no `prev` when removing `head`

Straightforward solution:
```java
class LinkedList {
    class LinkedListNode {
        public int val;
        public LinkedListNode next;
        LinkedListNode(int val) {
            this.val = val;
        }
    }

    LinkedListNode head;
    public LinkedList() {
        head = null;
    }

    public void insertHead(int val) {
        LinkedListNode node = new LinkedListNode(val);
        node.next = head;
        head = node;
    }

    public int get(int index) {
        if (index < 0 || head == null) return -1;

        int currI = 0;
        LinkedListNode curr = head;

        while(curr.next != null && currI != index) {
            currI++;
            curr = curr.next;
        }

        if (index != currI) {
            return -1;
        }

        return curr.val;
    }

    public void insertTail(int val) {
        if (head == null) {
            head = new LinkedListNode(val);
            return;
        }

        LinkedListNode curr = head;
        while (curr.next != null) {
            curr = curr.next;
        }

        curr.next = new LinkedListNode(val);
    }

    public boolean remove(int i) {
        if (i < 0 || head == null) return false;

        if (i == 0) {
            head = head.next;
            return true;
        }

        int currI = 0;
        LinkedListNode curr = head;
        LinkedListNode prev = null;

        while (curr.next != null && i != currI) {
            currI++;
            prev = curr;
            curr = curr.next;
        }

        // If got to end without finding
        if (i != currI) {
            return false;
        }
        
        prev.next = curr.next;
        return true;
    }

    public ArrayList<Integer> getValues() {
        ArrayList<Integer> list = new ArrayList<>();
        LinkedListNode curr = head;
        while(curr != null) {
            list.add(curr.val);
            curr = curr.next;
        }
        return list;
    }
}
```