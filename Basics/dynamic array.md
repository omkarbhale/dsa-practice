# Design Dynamic Array (Resizable Array)

Design a Dynamic Array (aka a resizable array) class, such as an `ArrayList` in Java or a `vector` in C++.

Your DynamicArray class should support the following operations:
- `DynamicArray(int capacity)` will initialize an empty array with a capacity of capacity, where capacity > 0.
- `int get(int i)` will return the element at index i. Assume that index i is valid.
- `void insert(int i, int n)` will insert the element n at index i. Assume that index i is valid.
- `void pushback(int n)` will push the element n to the end of the array.
- `int popback()` will pop and return the element at the end of the array. Assume that the array is non-empty.
- `void resize()` will double the capacity of the array.
- `int getSize()` will return the number of elements in the array.
- `int getCapacity()` will return the capacity of the array.

## Solution
Straightforward solution:
```java
class DynamicArray {
    private int size;
    private int[] data;
    private int capacity;

    DynamicArray(int capacity) {
        if (capacity <= 0) {
            capacity = 1;
        }
        this.capacity = capacity;
        this.size = 0;
        this.data = new int[capacity];
    }

    private void resize(int newcapacity) {
        assert newcapacity >= size;
        int[] newarr = new int[newcapacity];
        for (int i = 0; i < size; i++) {
            newarr[i] = data[i];
        }
        data = newarr;
        capacity = newcapacity;
    }

    int get(int i) {
        // Assume that i is valid
        return data[i];
    }

    void insert(int i, int n) {
        // Copy last element over
        pushback(data[size - 1]);

        // Copy all prev elements one forward
        for (int j = size - 2; j > i; j--) {
            data[j] = data[j - 1];
        }

        data[i] = n;
    }

    void pushback(int n) {
        if (size == capacity) {
            resize(capacity * 2);
        }

        data[size] = n;
        size++;
    }

    int popback() {
        // Assume non empty
        size--;
        return data[size];
    }

    void resize() {
        resize(capacity * 2);
    }

    int getSize() {
        return size;
    }

    int getCapacity() {
        return capacity;
    }

    @Override
    public String toString() {
        return Arrays.toString(data);
    }
}
```
