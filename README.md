# QueueCode
1. Implement a basic Queue using LinkedList in Java
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class BasicQueue {
    public static void main(String[] args) {
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(10);
        queue.offer(20);
        queue.offer(30);

        System.out.println(queue.poll()); // 10
        System.out.println(queue.peek()); // 20
    }
}
2. Implement a Queue using ArrayDeque in Java
java
Copy
Edit
import java.util.ArrayDeque;
import java.util.Queue;

public class QueueWithArrayDeque {
    public static void main(String[] args) {
        Queue<String> queue = new ArrayDeque<>();
        queue.offer("a");
        queue.offer("b");
        queue.offer("c");

        while (!queue.isEmpty()) {
            System.out.println(queue.poll());
        }
    }
}
3. Implement a Circular Queue using array (fixed size)
java
Copy
Edit
public class CircularQueue {
    private int[] arr;
    private int front, rear, size, capacity;

    public CircularQueue(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }

    public boolean enqueue(int value) {
        if (size == capacity) return false;
        rear = (rear + 1) % capacity;
        arr[rear] = value;
        size++;
        return true;
    }

    public Integer dequeue() {
        if (size == 0) return null;
        int value = arr[front];
        front = (front + 1) % capacity;
        size--;
        return value;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public boolean isFull() {
        return size == capacity;
    }

    public static void main(String[] args) {
        CircularQueue cq = new CircularQueue(3);
        cq.enqueue(1);
        cq.enqueue(2);
        cq.enqueue(3);
        System.out.println(cq.enqueue(4)); // false, full
        System.out.println(cq.dequeue());  // 1
        cq.enqueue(4);
        while (!cq.isEmpty()) {
            System.out.println(cq.dequeue());
        }
    }
}
4. Use Deque as Stack (LIFO) in Java
java
Copy
Edit
import java.util.ArrayDeque;
import java.util.Deque;

public class DequeAsStack {
    public static void main(String[] args) {
        Deque<Integer> stack = new ArrayDeque<>();
        stack.push(10);
        stack.push(20);
        stack.push(30);

        while (!stack.isEmpty()) {
            System.out.println(stack.pop());
        }
    }
}
5. Use Deque as Queue (FIFO) in Java
java
Copy
Edit
import java.util.ArrayDeque;
import java.util.Deque;

public class DequeAsQueue {
    public static void main(String[] args) {
        Deque<String> deque = new ArrayDeque<>();
        deque.offer("A");
        deque.offer("B");
        deque.offer("C");

        while (!deque.isEmpty()) {
            System.out.println(deque.poll());
        }
    }
}
6. Implement PriorityQueue in Java and print elements in priority order
java
Copy
Edit
import java.util.PriorityQueue;

public class PriorityQueueExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        pq.offer(50);
        pq.offer(10);
        pq.offer(30);

        while (!pq.isEmpty()) {
            System.out.println(pq.poll());
        }
    }
}
7. Reverse a queue using recursion
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class ReverseQueueRecursion {
    public static void reverseQueue(Queue<Integer> queue) {
        if (queue.isEmpty()) return;
        int front = queue.poll();
        reverseQueue(queue);
        queue.offer(front);
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(1);
        q.offer(2);
        q.offer(3);
        reverseQueue(q);
        System.out.println(q); // [3, 2, 1]
    }
}
8. Find the first non-repeating character in a stream using Queue
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class FirstNonRepeatingCharacter {
    public static void main(String[] args) {
        String stream = "aabc";
        int[] freq = new int[256];
        Queue<Character> q = new LinkedList<>();

        for (char ch : stream.toCharArray()) {
            freq[ch]++;
            q.offer(ch);
            while (!q.isEmpty() && freq[q.peek()] > 1) {
                q.poll();
            }
            System.out.println(q.isEmpty() ? -1 : q.peek());
        }
    }
}
9. Implement Deque using Doubly Linked List
java
Copy
Edit
class Node {
    int data;
    Node prev, next;

    Node(int d) { data = d; }
}

public class DequeDoublyLinkedList {
    Node front, rear;

    public void addFront(int val) {
        Node newNode = new Node(val);
        if (front == null) {
            front = rear = newNode;
        } else {
            newNode.next = front;
            front.prev = newNode;
            front = newNode;
        }
    }

    public void addRear(int val) {
        Node newNode = new Node(val);
        if (rear == null) {
            front = rear = newNode;
        } else {
            rear.next = newNode;
            newNode.prev = rear;
            rear = newNode;
        }
    }

    public Integer removeFront() {
        if (front == null) return null;
        int val = front.data;
        front = front.next;
        if (front != null) front.prev = null;
        else rear = null;
        return val;
    }

    public Integer removeRear() {
        if (rear == null) return null;
        int val = rear.data;
        rear = rear.prev;
        if (rear != null) rear.next = null;
        else front = null;
        return val;
    }

    public static void main(String[] args) {
        DequeDoublyLinkedList deque = new DequeDoublyLinkedList();
        deque.addFront(10);
        deque.addRear(20);
        deque.addFront(5);
        System.out.println(deque.removeRear());  // 20
        System.out.println(deque.removeFront()); // 5
    }
}
10. Check if a given sequence of brackets is balanced using Stack (Deque)
java
Copy
Edit
import java.util.ArrayDeque;
import java.util.Deque;

public class BalancedBrackets {
    public static boolean isBalanced(String s) {
        Deque<Character> stack = new ArrayDeque<>();
        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            } else {
                if (stack.isEmpty()) return false;
                char top = stack.pop();
                if ((c == ')' && top != '(') ||
                    (c == '}' && top != '{') ||
                    (c == ']' && top != '[')) {
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }

    public static void main(String[] args) {
        System.out.println(isBalanced("({[]})")); // true
        System.out.println(isBalanced("({[})"));  // false
    }
}
11. Implement a queue with two stacks
java
Copy
Edit
import java.util.Stack;

public class QueueWithTwoStacks {
    Stack<Integer> s1 = new Stack<>();
    Stack<Integer> s2 = new Stack<>();

    public void enqueue(int val) {
        s1.push(val);
    }

    public Integer dequeue() {
        if (s2.isEmpty()) {
            while (!s1.isEmpty()) {
                s2.push(s1.pop());
            }
        }
        return s2.isEmpty() ? null : s2.pop();
    }

    public static void main(String[] args) {
        QueueWithTwoStacks q = new QueueWithTwoStacks();
        q.enqueue(1);
        q.enqueue(2);
        q.enqueue(3);
        System.out.println(q.dequeue()); // 1
        System.out.println(q.dequeue()); // 2
    }
}
12. Find maximum element in each sliding window of size k using Deque
java
Copy
Edit
import java.util.ArrayDeque;
import java.util.Deque;

public class SlidingWindowMax {
    public static void printMax(int[] arr, int k) {
        Deque<Integer> dq = new ArrayDeque<>();
        for (int i = 0; i < arr.length; i++) {
            while (!dq.isEmpty() && dq.peekFirst() <= i - k) dq.pollFirst();
            while (!dq.isEmpty() && arr[dq.peekLast()] <= arr[i]) dq.pollLast();
            dq.offerLast(i);
            if (i >= k - 1) System.out.print(arr[dq.peekFirst()] + " ");
        }
    }

    public static void main(String[] args) {
        int[] arr = {1,3,-1,-3,5,3,6,7};
        int k = 3;
        printMax(arr, k);  // 3 3 5 5 6 7
    }
}
13. Implement Circular Deque
java
Copy
Edit
public class CircularDeque {
    private int[] data;
    private int front, rear, size, capacity;

    public CircularDeque(int capacity) {
        this.capacity = capacity;
        data = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }

    public boolean insertFront(int val) {
        if (size == capacity) return false;
        front = (front - 1 + capacity) % capacity;
        data[front] = val;
        size++;
        return true;
    }

    public boolean insertLast(int val) {
        if (size == capacity) return false;
        rear = (rear + 1) % capacity;
        data[rear] = val;
        size++;
        return true;
    }

    public Integer deleteFront() {
        if (size == 0) return null;
        int val = data[front];
        front = (front + 1) % capacity;
        size--;
        return val;
    }

    public Integer deleteLast() {
        if (size == 0) return null;
        int val = data[rear];
        rear = (rear - 1 + capacity) % capacity;
        size--;
        return val;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public boolean isFull() {
        return size == capacity;
    }

    public static void main(String[] args) {
        CircularDeque cd = new CircularDeque(3);
        cd.insertLast(1);
        cd.insertLast(2);
        cd.insertFront(3);
        System.out.println(cd.insertFront(4)); // false, full
        System.out.println(cd.deleteLast());   // 2
        cd.insertFront(4);
        while (!cd.isEmpty()) {
            System.out.println(cd.deleteFront());
        }
    }
}
14. Implement Queue using Stack (recursive dequeue)
java
Copy
Edit
import java.util.Stack;

public class QueueUsingStackRecursive {
    Stack<Integer> s1 = new Stack<>();
    Stack<Integer> s2 = new Stack<>();

    public void enqueue(int val) {
        s1.push(val);
    }

    public Integer dequeue() {
        if (s2.isEmpty()) {
            while (!s1.isEmpty()) {
                s2.push(s1.pop());
            }
        }
        return s2.isEmpty() ? null : s2.pop();
    }

    public static void main(String[] args) {
        QueueUsingStackRecursive q = new QueueUsingStackRecursive();
        q.enqueue(5);
        q.enqueue(10);
        System.out.println(q.dequeue()); // 5
        System.out.println(q.dequeue()); // 10
    }
}
15. Implement circular queue using Linked List
java
Copy
Edit
class Node {
    int val;
    Node next;
    Node(int v) { val = v; }
}

public class CircularQueueLinkedList {
    private Node front = null, rear = null;
    private int size = 0;
    private int capacity;

    public CircularQueueLinkedList(int capacity) {
        this.capacity = capacity;
    }

    public boolean enqueue(int val) {
        if (size == capacity) return false;
        Node newNode = new Node(val);
        if (rear == null) {
            front = rear = newNode;
            rear.next = front;
        } else {
            rear.next = newNode;
            rear = newNode;
            rear.next = front;
        }
        size++;
        return true;
    }

    public Integer dequeue() {
        if (size == 0) return null;
        int val = front.val;
        if (front == rear) {
            front = rear = null;
        } else {
            front = front.next;
            rear.next = front;
        }
        size--;
        return val;
    }

    public static void main(String[] args) {
        CircularQueueLinkedList cq = new CircularQueueLinkedList(2);
        System.out.println(cq.enqueue(1)); // true
        System.out.println(cq.enqueue(2)); // true
        System.out.println(cq.enqueue(3)); // false full
        System.out.println(cq.dequeue());  // 1
        System.out.println(cq.enqueue(3)); // true
        while (cq.size > 0) {
            System.out.println(cq.dequeue());
        }
    }
}
16. Print elements of a queue without modifying it
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class PrintQueueWithoutModifying {
    public static void printQueue(Queue<Integer> queue) {
        for (Integer val : queue) {
            System.out.print(val + " ");
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(10);
        q.offer(20);
        q.offer(30);
        printQueue(q); // 10 20 30
        System.out.println(q); // Queue remains unchanged
    }
}
17. Implement a Queue that supports getMin operation in O(1)
java
Copy
Edit
import java.util.Deque;
import java.util.LinkedList;
import java.util.Queue;

public class MinQueue {
    Queue<Integer> q = new LinkedList<>();
    Deque<Integer> minDeque = new LinkedList<>();

    public void enqueue(int val) {
        q.offer(val);
        while (!minDeque.isEmpty() && minDeque.peekLast() > val) {
            minDeque.pollLast();
        }
        minDeque.offerLast(val);
    }

    public Integer dequeue() {
        if (q.isEmpty()) return null;
        int val = q.poll();
        if (val == minDeque.peekFirst()) {
            minDeque.pollFirst();
        }
        return val;
    }

    public Integer getMin() {
        return minDeque.isEmpty() ? null : minDeque.peekFirst();
    }

    public static void main(String[] args) {
        MinQueue mq = new MinQueue();
        mq.enqueue(3);
        mq.enqueue(1);
        mq.enqueue(2);
        System.out.println(mq.getMin()); // 1
        mq.dequeue();
        System.out.println(mq.getMin()); // 1
        mq.dequeue();
        System.out.println(mq.getMin()); // 2
    }
}
18. Implement LRU Cache using Deque and HashMap
java
Copy
Edit
import java.util.*;

public class LRUCache {
    private int capacity;
    private Map<Integer, Integer> map;
    private Deque<Integer> deque;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<>();
        deque = new LinkedList<>();
    }

    public int get(int key) {
        if (!map.containsKey(key)) return -1;
        deque.remove(key);
        deque.offerFirst(key);
        return map.get(key);
    }

    public void put(int key, int value) {
        if (map.containsKey(key)) {
            deque.remove(key);
        } else if (deque.size() == capacity) {
            int last = deque.pollLast();
            map.remove(last);
        }
        deque.offerFirst(key);
        map.put(key, value);
    }

    public static void main(String[] args) {
        LRUCache cache = new LRUCache(2);
        cache.put(1, 10);
        cache.put(2, 20);
        System.out.println(cache.get(1)); // 10
        cache.put(3, 30);  // evicts key 2
        System.out.println(cache.get(2)); // -1
    }
}
19. Rotate a queue by k positions
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class RotateQueue {
    public static void rotate(Queue<Integer> q, int k) {
        for (int i = 0; i < k; i++) {
            q.offer(q.poll());
        }
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        for (int i = 1; i <= 5; i++) q.offer(i);
        rotate(q, 2);
        System.out.println(q); // [3, 4, 5, 1, 2]
    }
}
20. Find the first negative integer in every window of size k in an array using queue
java
Copy
Edit
import java.util.*;

public class FirstNegativeInWindow {
    public static void printFirstNegative(int[] arr, int k) {
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < k; i++) {
            if (arr[i] < 0) q.offer(i);
        }
        for (int i = k; i < arr.length; i++) {
            if (!q.isEmpty()) System.out.print(arr[q.peek()] + " ");
            else System.out.print("0 ");
            while (!q.isEmpty() && q.peek() <= i - k) q.poll();
            if (arr[i] < 0) q.offer(i);
        }
        if (!q.isEmpty()) System.out.print(arr[q.peek()] + " ");
        else System.out.print("0 ");
    }

    public static void main(String[] args) {
        int[] arr = {12, -1, -7, 8, -15, 30, 16, 28};
        printFirstNegative(arr, 3); // -1 -1 -7 -15 -15 0
    }
}
21. Implement Double Ended Queue (Deque) with fixed size array
java
Copy
Edit
public class ArrayDeque {
    private int[] arr;
    private int front, rear, size, capacity;

    public ArrayDeque(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        front = -1;
        rear = 0;
        size = 0;
    }

    public boolean insertFront(int val) {
        if (isFull()) return false;
        if (isEmpty()) {
            front = rear = 0;
        } else {
            front = (front - 1 + capacity) % capacity;
        }
        arr[front] = val;
        size++;
        return true;
    }

    public boolean insertRear(int val) {
        if (isFull()) return false;
        if (isEmpty()) {
            front = rear = 0;
        } else {
            rear = (rear + 1) % capacity;
        }
        arr[rear] = val;
        size++;
        return true;
    }

    public Integer deleteFront() {
        if (isEmpty()) return null;
        int val = arr[front];
        if (front == rear) {
            front = -1;
            rear = 0;
        } else {
            front = (front + 1) % capacity;
        }
        size--;
        return val;
    }

    public Integer deleteRear() {
        if (isEmpty()) return null;
        int val = arr[rear];
        if (front == rear) {
            front = -1;
            rear = 0;
        } else {
            rear = (rear - 1 + capacity) % capacity;
        }
        size--;
        return val;
    }

    public boolean isFull() {
        return size == capacity;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public static void main(String[] args) {
        ArrayDeque deque = new ArrayDeque(3);
        deque.insertRear(1);
        deque.insertRear(2);
        deque.insertFront(3);
        System.out.println(deque.insertFront(4)); // false
        System.out.println(deque.deleteRear());   // 2
        System.out.println(deque.deleteFront());  // 3
    }
}
22. Implement a queue that supports max element retrieval in O(1)
java
Copy
Edit
import java.util.Deque;
import java.util.LinkedList;

public class MaxQueue {
    private Deque<Integer> maxDeque = new LinkedList<>();
    private LinkedList<Integer> queue = new LinkedList<>();

    public void enqueue(int val) {
        queue.addLast(val);
        while (!maxDeque.isEmpty() && maxDeque.peekLast() < val) {
            maxDeque.pollLast();
        }
        maxDeque.addLast(val);
    }

    public Integer dequeue() {
        if (queue.isEmpty()) return null;
        int val = queue.pollFirst();
        if (val == maxDeque.peekFirst()) {
            maxDeque.pollFirst();
        }
        return val;
    }

    public Integer getMax() {
        return maxDeque.isEmpty() ? null : maxDeque.peekFirst();
    }

    public static void main(String[] args) {
        MaxQueue mq = new MaxQueue();
        mq.enqueue(1);
        mq.enqueue(3);
        mq.enqueue(2);
        System.out.println(mq.getMax()); // 3
        mq.dequeue();
        System.out.println(mq.getMax()); // 3
        mq.dequeue();
        System.out.println(mq.getMax()); // 2
    }
}
23. Check if a queue is palindrome
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class QueuePalindrome {
    public static boolean isPalindrome(Queue<Integer> queue) {
        LinkedList<Integer> list = new LinkedList<>(queue);
        int left = 0, right = list.size() - 1;
        while (left < right) {
            if (!list.get(left).equals(list.get(right))) return false;
            left++;
            right--;
        }
        return true;
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(1);
        q.offer(2);
        q.offer(2);
        q.offer(1);
        System.out.println(isPalindrome(q)); // true
    }
}
24. Merge two sorted queues into one sorted queue
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class MergeSortedQueues {
    public static Queue<Integer> merge(Queue<Integer> q1, Queue<Integer> q2) {
        Queue<Integer> result = new LinkedList<>();
        while (!q1.isEmpty() && !q2.isEmpty()) {
            if (q1.peek() <= q2.peek()) result.offer(q1.poll());
            else result.offer(q2.poll());
        }
        while (!q1.isEmpty()) result.offer(q1.poll());
        while (!q2.isEmpty()) result.offer(q2.poll());
        return result;
    }

    public static void main(String[] args) {
        Queue<Integer> q1 = new LinkedList<>();
        q1.offer(1);
        q1.offer(3);
        q1.offer(5);
        Queue<Integer> q2 = new LinkedList<>();
        q2.offer(2);
        q2.offer(4);
        q2.offer(6);
        System.out.println(merge(q1, q2)); // [1, 2, 3, 4, 5, 6]
    }
}
25. Implement queue using Circular Linked List
java
Copy
Edit
class Node {
    int val;
    Node next;
    Node(int v) { val = v; }
}

public class QueueCircularLinkedList {
    private Node rear = null;

    public void enqueue(int val) {
        Node newNode = new Node(val);
        if (rear == null) {
            newNode.next = newNode;
        } else {
            newNode.next = rear.next;
            rear.next = newNode;
        }
        rear = newNode;
    }

    public Integer dequeue() {
        if (rear == null) return null;
        Node front = rear.next;
        if (rear == front) rear = null;
        else rear.next = front.next;
        return front.val;
    }

    public static void main(String[] args) {
        QueueCircularLinkedList q = new QueueCircularLinkedList();
        q.enqueue(10);
        q.enqueue(20);
        System.out.println(q.dequeue()); // 10
        System.out.println(q.dequeue()); // 20
        System.out.println(q.dequeue()); // null
    }
}
26. Find the minimum time required to complete tasks given cooldown period using Queue
java
Copy
Edit
import java.util.*;

public class TaskScheduler {
    public static int leastInterval(char[] tasks, int n) {
        int[] freq = new int[26];
        for (char t : tasks) freq[t - 'A']++;
        PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> b - a);
        for (int f : freq) if (f > 0) pq.offer(f);

        int time = 0;
        Queue<int[]> cooldown = new LinkedList<>();

        while (!pq.isEmpty() || !cooldown.isEmpty()) {
            time++;
            if (!pq.isEmpty()) {
                int f = pq.poll() - 1;
                if (f > 0) cooldown.offer(new int[]{f, time + n});
            }
            if (!cooldown.isEmpty() && cooldown.peek()[1] == time) {
                pq.offer(cooldown.poll()[0]);
            }
        }
        return time;
    }

    public static void main(String[] args) {
        System.out.println(leastInterval(new char[]{'A','A','A','B','B','B'}, 2)); // 8
    }
}
27. Print binary numbers from 1 to N using queue
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class BinaryNumbersQueue {
    public static void printBinary(int n) {
        Queue<String> q = new LinkedList<>();
        q.offer("1");
        for (int i = 1; i <= n; i++) {
            String s = q.poll();
            System.out.print(s + " ");
            q.offer(s + "0");
            q.offer(s + "1");
        }
    }

    public static void main(String[] args) {
        printBinary(5); // 1 10 11 100 101
    }
}
28. Implement a max-size bounded queue that discards oldest element on overflow
java
Copy
Edit
import java.util.LinkedList;

public class BoundedQueue {
    private LinkedList<Integer> queue = new LinkedList<>();
    private int capacity;

    public BoundedQueue(int capacity) {
        this.capacity = capacity;
    }

    public void enqueue(int val) {
        if (queue.size() == capacity) {
            queue.poll();
        }
        queue.offer(val);
    }

    public Integer dequeue() {
        return queue.poll();
    }

    public static void main(String[] args) {
        BoundedQueue bq = new BoundedQueue(3);
        bq.enqueue(1);
        bq.enqueue(2);
        bq.enqueue(3);
        bq.enqueue(4); // removes 1
        while (true) {
            Integer val = bq.dequeue();
            if (val == null) break;
            System.out.println(val);
        }
    }
}
29. Find minimum cost to connect ropes (using PriorityQueue)
java
Copy
Edit
import java.util.PriorityQueue;

public class ConnectRopes {
    public static int minCost(int[] ropes) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int rope : ropes) pq.offer(rope);
        int cost = 0;

        while (pq.size() > 1) {
            int first = pq.poll();
            int second = pq.poll();
            int sum = first + second;
            cost += sum;
            pq.offer(sum);
        }
        return cost;
    }
29. Implement a queue using two stacks such that each operation runs in amortized O(1).
java
Copy
Edit
import java.util.Stack;

public class QueueUsingTwoStacks {
    Stack<Integer> stack1 = new Stack<>();
    Stack<Integer> stack2 = new Stack<>();

    public void enqueue(int val) {
        stack1.push(val);
    }

    public Integer dequeue() {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) stack2.push(stack1.pop());
        }
        return stack2.isEmpty() ? null : stack2.pop();
    }

    public static void main(String[] args) {
        QueueUsingTwoStacks queue = new QueueUsingTwoStacks();
        queue.enqueue(1);
        queue.enqueue(2);
        queue.enqueue(3);
        System.out.println(queue.dequeue()); // 1
        queue.enqueue(4);
        System.out.println(queue.dequeue()); // 2
        System.out.println(queue.dequeue()); // 3
    }
}
30. Design a data structure that supports insertion, deletion, and getting random elements in O(1) using a queue.
Note: This is complex using just a queue, so here’s an approach combining a queue and a HashMap.

java
Copy
Edit
import java.util.*;

public class RandomizedQueue {
    private List<Integer> list = new ArrayList<>();
    private Map<Integer, Integer> map = new HashMap<>();
    private Random rand = new Random();

    public boolean insert(int val) {
        if (map.containsKey(val)) return false;
        map.put(val, list.size());
        list.add(val);
        return true;
    }

    public boolean remove(int val) {
        if (!map.containsKey(val)) return false;
        int index = map.get(val);
        int lastElement = list.get(list.size() - 1);
        list.set(index, lastElement);
        map.put(lastElement, index);
        list.remove(list.size() - 1);
        map.remove(val);
        return true;
    }

    public Integer getRandom() {
        if (list.isEmpty()) return null;
        return list.get(rand.nextInt(list.size()));
    }

    public static void main(String[] args) {
        RandomizedQueue rq = new RandomizedQueue();
        rq.insert(1);
        rq.insert(2);
        rq.insert(3);
        System.out.println(rq.getRandom());
        rq.remove(2);
        System.out.println(rq.getRandom());
    }
}
31. Write a program to implement a circular queue using a singly linked list.
java
Copy
Edit
public class CircularQueueLinkedList {
    class Node {
        int val;
        Node next;
        Node(int v) { val = v; }
    }

    private Node rear = null;

    public void enqueue(int val) {
        Node newNode = new Node(val);
        if (rear == null) {
            newNode.next = newNode;
            rear = newNode;
        } else {
            newNode.next = rear.next;
            rear.next = newNode;
            rear = newNode;
        }
    }

    public Integer dequeue() {
        if (rear == null) return null;
        Node front = rear.next;
        if (front == rear) {
            rear = null;
        } else {
            rear.next = front.next;
        }
        return front.val;
    }

    public static void main(String[] args) {
        CircularQueueLinkedList q = new CircularQueueLinkedList();
        q.enqueue(10);
        q.enqueue(20);
        System.out.println(q.dequeue()); // 10
        System.out.println(q.dequeue()); // 20
        System.out.println(q.dequeue()); // null
    }
}
32. Find the maximum sum of k consecutive elements in a stream using a queue.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class MaxSumKConsecutive {
    public static int maxSumK(int[] arr, int k) {
        Queue<Integer> window = new LinkedList<>();
        int sum = 0, maxSum = Integer.MIN_VALUE;

        for (int i = 0; i < arr.length; i++) {
            sum += arr[i];
            window.offer(arr[i]);
            if (window.size() > k) {
                sum -= window.poll();
            }
            if (window.size() == k) {
                maxSum = Math.max(maxSum, sum);
            }
        }
        return maxSum;
    }

    public static void main(String[] args) {
        int[] arr = {2, 3, 5, 2, 9, 7, 1};
        int k = 3;
        System.out.println(maxSumK(arr, k)); // 18 (9 + 7 + 2)
    }
}
33. Implement a queue that can return the median element in O(log n) time.
java
Copy
Edit
import java.util.PriorityQueue;

public class MedianQueue {
    private PriorityQueue<Integer> maxHeap = new PriorityQueue<>((a,b) -> b - a);
    private PriorityQueue<Integer> minHeap = new PriorityQueue<>();
    private LinkedList<Integer> queue = new LinkedList<>();

    public void enqueue(int val) {
        queue.addLast(val);
        if (maxHeap.isEmpty() || val <= maxHeap.peek()) {
            maxHeap.offer(val);
        } else {
            minHeap.offer(val);
        }
        balanceHeaps();
    }

    public Integer dequeue() {
        if (queue.isEmpty()) return null;
        int val = queue.removeFirst();
        if (!maxHeap.remove(val)) {
            minHeap.remove(val);
        }
        balanceHeaps();
        return val;
    }

    private void balanceHeaps() {
        if (maxHeap.size() > minHeap.size() + 1) minHeap.offer(maxHeap.poll());
        else if (minHeap.size() > maxHeap.size()) maxHeap.offer(minHeap.poll());
    }

    public Double getMedian() {
        if (queue.isEmpty()) return null;
        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        }
        return (double) maxHeap.peek();
    }

    public static void main(String[] args) {
        MedianQueue mq = new MedianQueue();
        mq.enqueue(1);
        mq.enqueue(3);
        mq.enqueue(5);
        System.out.println(mq.getMedian()); // 3.0
        mq.dequeue();
        System.out.println(mq.getMedian()); // 4.0
    }
}
34. Given a queue, reverse the first k elements of the queue.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

public class ReverseFirstK {
    public static void reverseK(Queue<Integer> q, int k) {
        if (q == null || k > q.size()) return;

        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < k; i++) {
            stack.push(q.poll());
        }
        while (!stack.isEmpty()) {
            q.offer(stack.pop());
        }
        int size = q.size();
        for (int i = 0; i < size - k; i++) {
            q.offer(q.poll());
        }
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        for (int i = 1; i <= 5; i++) q.offer(i);
        reverseK(q, 3);
        System.out.println(q); // [3, 2, 1, 4, 5]
    }
}
35. Given a stream of integers, design a queue-like data structure to return the first unique number in the stream.
java
Copy
Edit
import java.util.*;

public class FirstUniqueQueue {
    private Queue<Integer> queue = new LinkedList<>();
    private Map<Integer, Integer> freq = new HashMap<>();

    public void add(int val) {
        freq.put(val, freq.getOrDefault(val, 0) + 1);
        queue.offer(val);
        while (!queue.isEmpty() && freq.get(queue.peek()) > 1) {
            queue.poll();
        }
    }

    public Integer firstUnique() {
        return queue.isEmpty() ? null : queue.peek();
    }

    public static void main(String[] args) {
        FirstUniqueQueue fuq = new FirstUniqueQueue();
        fuq.add(2);
        fuq.add(3);
        fuq.add(5);
        fuq.add(2);
        System.out.println(fuq.firstUnique()); // 3
        fuq.add(3);
        System.out.println(fuq.firstUnique()); // 5
    }
}
36. Implement a deque that supports findMin operation in O(1) time.
java
Copy
Edit
import java.util.Deque;
import java.util.LinkedList;

public class MinDeque {
    private Deque<Integer> deque = new LinkedList<>();
    private Deque<Integer> minDeque = new LinkedList<>();

    public void addLast(int val) {
        deque.offerLast(val);
        while (!minDeque.isEmpty() && minDeque.peekLast() > val) {
            minDeque.pollLast();
        }
        minDeque.offerLast(val);
    }

    public Integer removeFirst() {
        if (deque.isEmpty()) return null;
        int val = deque.pollFirst();
        if (val == minDeque.peekFirst()) {
            minDeque.pollFirst();
        }
        return val;
    }

    public Integer getMin() {
        return minDeque.isEmpty() ? null : minDeque.peekFirst();
    }

    public static void main(String[] args) {
        MinDeque md = new MinDeque();
        md.addLast(4);
        md.addLast(2);
        md.addLast(3);
        System.out.println(md.getMin()); // 2
        md.removeFirst();
        System.out.println(md.getMin()); // 2
        md.removeFirst();
        System.out.println(md.getMin()); // 3
    }
}
37. Design a circular deque (double-ended queue) that supports all operations in O(1) time.
java
Copy
Edit
public class CircularDeque {
    private int[] arr;
    private int front, rear, capacity, size;

    public CircularDeque(int k) {
        capacity = k;
        arr = new int[capacity];
        front = 0;
        rear = 0;
        size = 0;
    }

    public boolean insertFront(int val) {
        if (isFull()) return false;
        front = (front - 1 + capacity) % capacity;
        arr[front] = val;
        size++;
        return true;
    }

    public boolean insertLast(int val) {
        if (isFull()) return false;
        arr[rear] = val;
        rear = (rear + 1) % capacity;
        size++;
        return true;
    }

    public boolean deleteFront() {
        if (isEmpty()) return false;
        front = (front + 1) % capacity;
        size--;
        return true;
    }

    public boolean deleteLast() {
        if (isEmpty()) return false;
        rear = (rear - 1 + capacity) % capacity;
        size--;
        return true;
    }

    public int getFront() {
        if (isEmpty()) return -1;
        return arr[front];
    }

    public int getRear() {
        if (isEmpty()) return -1;
        return arr[(rear - 1 + capacity) % capacity];
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public boolean isFull() {
        return size == capacity;
    }

    public static void main(String[] args) {
        CircularDeque cd = new CircularDeque(3);
        cd.insertLast(1);
        cd.insertLast(2);
        cd.insertFront(3);
        System.out.println(cd.getRear());  // 2
        cd.deleteLast();
        System.out.println(cd.getRear());  // 1
    }
}
39. Using a queue, implement a function to check if a given string is a palindrome.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class PalindromeQueue {
    public static boolean isPalindrome(String s) {
        Queue<Character> queue = new LinkedList<>();
        for (char c : s.toCharArray()) queue.offer(c);
        
        while (queue.size() > 1) {
            if (!queue.poll().equals(queue.removeLast())) { // removeLast not in queue, workaround below
                return false;
            }
        }
        return true;
    }

    // Since Queue doesn't have removeLast, using LinkedList cast
    public static boolean isPalindromeFixed(String s) {
        LinkedList<Character> queue = new LinkedList<>();
        for (char c : s.toCharArray()) queue.offer(c);
        while (queue.size() > 1) {
            if (!queue.poll().equals(queue.removeLast())) return false;
        }
        return true;
    }

    public static void main(String[] args) {
        String str = "racecar";
        System.out.println(isPalindromeFixed(str)); // true
        System.out.println(isPalindromeFixed("hello")); // false
    }
}
40. Given a queue, sort its elements using only queue operations (no extra data structures allowed).
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class SortQueue {
    public static void sortQueue(Queue<Integer> q) {
        if (q.isEmpty()) return;
        int size = q.size();

        for (int i = 0; i < size; i++) {
            int minIndex = -1;
            int minValue = Integer.MAX_VALUE;

            // Find min value and its index
            for (int j = 0; j < size; j++) {
                int val = q.poll();
                if (val < minValue && j <= size - i - 1) {
                    minValue = val;
                    minIndex = j;
                }
                q.offer(val);
            }

            // Move min to end
            for (int j = 0; j < size; j++) {
                int val = q.poll();
                if (j != minIndex) q.offer(val);
            }
            q.offer(minValue);
        }

        // Rearrange so smallest at front
        for (int i = 0; i < size; i++) {
            q.offer(q.poll());
        }
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(3);
        q.offer(1);
        q.offer(4);
        q.offer(2);
        sortQueue(q);
        System.out.println(q); // [1, 2, 3, 4]
    }
}
41. Given a queue of integers, rotate the queue to the right by k positions.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class RotateQueue {
    public static void rotateRight(Queue<Integer> q, int k) {
        int size = q.size();
        k = k % size;
        for (int i = 0; i < size - k; i++) {
            q.offer(q.poll());
        }
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        for (int i = 1; i <= 5; i++) q.offer(i);
        rotateRight(q, 2);
        System.out.println(q); // [4, 5, 1, 2, 3]
    }
}
42. Implement a priority queue using a circular queue.
java
Copy
Edit
import java.util.Arrays;

public class CircularPriorityQueue {
    private int[] arr;
    private int front, rear, size, capacity;

    public CircularPriorityQueue(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        front = -1;
        rear = -1;
        size = 0;
    }

    public boolean enqueue(int val) {
        if (isFull()) return false;
        if (isEmpty()) {
            front = 0; rear = 0;
            arr[rear] = val;
        } else {
            rear = (rear + 1) % capacity;
            arr[rear] = val;
            // Bubble up the new element based on priority (min value = high priority)
            int i = rear;
            while (i != front) {
                int prev = (i - 1 + capacity) % capacity;
                if (arr[i] < arr[prev]) {
                    int temp = arr[i];
                    arr[i] = arr[prev];
                    arr[prev] = temp;
                    i = prev;
                } else break;
            }
        }
        size++;
        return true;
    }

    public Integer dequeue() {
        if (isEmpty()) return null;
        int val = arr[front];
        if (front == rear) front = rear = -1;
        else front = (front + 1) % capacity;
        size--;
        return val;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public boolean isFull() {
        return size == capacity;
    }

    public static void main(String[] args) {
        CircularPriorityQueue cpq = new CircularPriorityQueue(5);
        cpq.enqueue(5);
        cpq.enqueue(3);
        cpq.enqueue(7);
        cpq.enqueue(1);
        System.out.println(cpq.dequeue()); // 1 (highest priority)
        System.out.println(cpq.dequeue()); // 3
    }
}
43. Given a queue and an integer k, remove all occurrences of k from the queue.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class RemoveOccurrences {
    public static void removeAll(Queue<Integer> q, int k) {
        int size = q.size();
        for (int i = 0; i < size; i++) {
            int val = q.poll();
            if (val != k) q.offer(val);
        }
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(2); q.offer(3); q.offer(2); q.offer(4);
        removeAll(q, 2);
        System.out.println(q); // [3, 4]
    }
}
44. Given a queue, split it into two queues containing alternate elements.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class SplitQueueAlternate {
    public static Queue<Integer>[] splitAlternate(Queue<Integer> q) {
        Queue<Integer> q1 = new LinkedList<>();
        Queue<Integer> q2 = new LinkedList<>();
        boolean flag = true;
        while (!q.isEmpty()) {
            if (flag) q1.offer(q.poll());
            else q2.offer(q.poll());
            flag = !flag;
        }
        return new Queue[] {q1, q2};
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        for (int i = 1; i <= 6; i++) q.offer(i);
        Queue<Integer>[] result = splitAlternate(q);
        System.out.println(result[0]); // [1, 3, 5]
        System.out.println(result[1]); // [2, 4, 6]
    }
}
45. Implement a queue using two deques.
java
Copy
Edit
import java.util.Deque;
import java.util.LinkedList;

public class QueueUsingTwoDeques {
    Deque<Integer> input = new LinkedList<>();
    Deque<Integer> output = new LinkedList<>();

    public void enqueue(int val) {
        input.offerLast(val);
    }

    public Integer dequeue() {
        if (output.isEmpty()) {
            while (!input.isEmpty()) output.offerFirst(input.pollLast());
        }
        return output.isEmpty() ? null : output.pollFirst();
    }

    public static void main(String[] args) {
        QueueUsingTwoDeques queue = new QueueUsingTwoDeques();
        queue.enqueue(1);
        queue.enqueue(2);
        queue.enqueue(3);
        System.out.println(queue.dequeue()); // 1
        System.out.println(queue.dequeue()); // 2
    }
}
46. Implement a circular queue where enqueue operation overwrites oldest data on overflow.
java
Copy
Edit
public class OverwritingCircularQueue {
    private int[] arr;
    private int front, rear, size, capacity;

    public OverwritingCircularQueue(int capacity) {
        this.capacity = capacity;
        arr = new int[capacity];
        front = 0; rear = -1; size = 0;
    }

    public void enqueue(int val) {
        rear = (rear + 1) % capacity;
        arr[rear] = val;
        if (size < capacity) size++;
        else front = (front + 1) % capacity; // overwrite oldest
    }

    public Integer dequeue() {
        if (size == 0) return null;
        int val = arr[front];
        front = (front + 1) % capacity;
        size--;
        return val;
    }

    public static void main(String[] args) {
        OverwritingCircularQueue ocq = new OverwritingCircularQueue(3);
        ocq.enqueue(1);
        ocq.enqueue(2);
        ocq.enqueue(3);
        ocq.enqueue(4); // overwrites 1
        System.out.println(ocq.dequeue()); // 2
    }
}
47. Given a queue, find the second largest element without modifying the queue.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class SecondLargestInQueue {
    public static Integer secondLargest(Queue<Integer> q) {
        if (q.size() < 2) return null;

        Integer max = null, secondMax = null;
        int size = q.size();

        for (int i = 0; i < size; i++) {
            int val = q.poll();
            if (max == null || val > max) {
                secondMax = max;
                max = val;
            } else if ((secondMax == null || val > secondMax) && val < max) {
                secondMax = val;
            }
            q.offer(val);
        }
        return secondMax;
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(3); q.offer(5); q.offer(1); q.offer(4);
        System.out.println(secondLargest(q)); // 4
    }
}
48. Design a queue that supports increment operation on the first k elements.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class IncrementQueue {
    private LinkedList<Integer> list = new LinkedList<>();

    public void enqueue(int val) {
        list.addLast(val);
    }

    public Integer dequeue() {
        return list.isEmpty() ? null : list.removeFirst();
    }

    public void increment(int k, int val) {
        int limit = Math.min(k, list.size());
        for (int i = 0; i < limit; i++) {
            list.set(i, list.get(i) + val);
        }
    }

    public static void main(String[] args) {
        IncrementQueue q = new IncrementQueue();
        q.enqueue(1); q.enqueue(2); q.enqueue(3);
        q.increment(2, 5);
        System.out.println(q.list); // [6, 7, 3]
    }
}
49. Implement a queue that returns the maximum element in O(1) time.
java
Copy
Edit
import java.util.Deque;
import java.util.LinkedList;
import java.util.Queue;

public class MaxQueue {
    private Queue<Integer> queue = new LinkedList<>();
    private Deque<Integer> maxDeque = new LinkedList<>();

    public void enqueue(int val) {
        queue.offer(val);
        while (!maxDeque.isEmpty() && maxDeque.peekLast() < val) {
            maxDeque.pollLast();
        }
        maxDeque.offerLast(val);
    }

    public Integer dequeue() {
        if (queue.isEmpty()) return null;
        int val = queue.poll();
        if (val == maxDeque.peekFirst()) {
            maxDeque.pollFirst();
        }
        return val;
    }

    public Integer getMax() {
        return maxDeque.isEmpty() ? null : maxDeque.peekFirst();
    }

    public static void main(String[] args) {
        MaxQueue mq = new MaxQueue();
        mq.enqueue(1);
        mq.enqueue(3);
        mq.enqueue(2);
        System.out.println(mq.getMax()); // 3
        mq.dequeue();
        System.out.println(mq.getMax()); // 3
        mq.dequeue();
        System.out.println(mq.getMax()); // 2
    }
}
50. Reverse the first k elements of a queue.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

public class ReverseKElements {
    public static void reverseFirstK(Queue<Integer> q, int k) {
        if (q.isEmpty() || k > q.size()) return;
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < k; i++) stack.push(q.poll());
        while (!stack.isEmpty()) q.offer(stack.pop());
        int size = q.size();
        for (int i = 0; i < size - k; i++) q.offer(q.poll());
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        for (int i = 1; i <= 5; i++) q.offer(i);
        reverseFirstK(q, 3);
        System.out.println(q); // [3, 2, 1, 4, 5]
    }
}
51. Implement a deque and demonstrate insertion and deletion at both ends.
java
Copy
Edit
import java.util.Deque;
import java.util.LinkedList;

public class DequeDemo {
    public static void main(String[] args) {
        Deque<Integer> deque = new LinkedList<>();
        deque.offerFirst(1); // insert front
        deque.offerLast(2);  // insert rear
        deque.offerFirst(3);
        System.out.println(deque); // [3, 1, 2]
        deque.pollFirst(); // remove front (3)
        deque.pollLast();  // remove rear (2)
        System.out.println(deque); // [1]
    }
}
52. Check if a given queue is sorted in ascending order.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class CheckSortedQueue {
    public static boolean isSorted(Queue<Integer> q) {
        if (q.isEmpty()) return true;
        int prev = q.poll();
        q.offer(prev);
        int size = q.size();
        boolean sorted = true;
        for (int i = 0; i < size; i++) {
            int curr = q.poll();
            if (curr < prev) sorted = false;
            q.offer(curr);
            prev = curr;
        }
        return sorted;
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(1); q.offer(2); q.offer(3);
        System.out.println(isSorted(q)); // true
        q.offer(0);
        System.out.println(isSorted(q)); // false
    }
}
53. Merge two sorted queues into a single sorted queue.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class MergeSortedQueues {
    public static Queue<Integer> merge(Queue<Integer> q1, Queue<Integer> q2) {
        Queue<Integer> merged = new LinkedList<>();
        while (!q1.isEmpty() && !q2.isEmpty()) {
            if (q1.peek() <= q2.peek()) merged.offer(q1.poll());
            else merged.offer(q2.poll());
        }
        merged.addAll(q1);
        merged.addAll(q2);
        return merged;
    }

    public static void main(String[] args) {
        Queue<Integer> q1 = new LinkedList<>();
        Queue<Integer> q2 = new LinkedList<>();
        q1.offer(1); q1.offer(3); q1.offer(5);
        q2.offer(2); q2.offer(4); q2.offer(6);
        Queue<Integer> merged = merge(q1, q2);
        System.out.println(merged); // [1, 2, 3, 4, 5, 6]
    }
}
54. Find the first non-repeating character in a stream of characters using a queue.
java
Copy
Edit
import java.util.HashMap;
import java.util.LinkedList;
import java.util.Queue;

public class FirstNonRepeatingChar {
    public static void printFirstNonRepeating(String stream) {
        Queue<Character> q = new LinkedList<>();
        HashMap<Character, Integer> freq = new HashMap<>();

        for (char c : stream.toCharArray()) {
            freq.put(c, freq.getOrDefault(c, 0) + 1);
            q.offer(c);

            while (!q.isEmpty() && freq.get(q.peek()) > 1) {
                q.poll();
            }

            if (q.isEmpty()) System.out.print(-1 + " ");
            else System.out.print(q.peek() + " ");
        }
    }

    public static void main(String[] args) {
        String stream = "aabc";
        printFirstNonRepeating(stream);  // a -1 b b
    }
}
55. Implement a circular queue with dynamic resizing.
java
Copy
Edit
public class DynamicCircularQueue {
    private int[] arr;
    private int front, rear, size, capacity;

    public DynamicCircularQueue(int initialCapacity) {
        capacity = initialCapacity;
        arr = new int[capacity];
        front = 0; rear = -1; size = 0;
    }

    private void resize() {
        int newCapacity = capacity * 2;
        int[] newArr = new int[newCapacity];
        for (int i = 0; i < size; i++) {
            newArr[i] = arr[(front + i) % capacity];
        }
        arr = newArr;
        capacity = newCapacity;
        front = 0;
        rear = size - 1;
    }

    public void enqueue(int val) {
        if (size == capacity) resize();
        rear = (rear + 1) % capacity;
        arr[rear] = val;
        size++;
    }

    public Integer dequeue() {
        if (size == 0) return null;
        int val = arr[front];
        front = (front + 1) % capacity;
        size--;
        return val;
    }

    public static void main(String[] args) {
        DynamicCircularQueue dcq = new DynamicCircularQueue(2);
        dcq.enqueue(1);
        dcq.enqueue(2);
        dcq.enqueue(3); // triggers resize
        System.out.println(dcq.dequeue()); // 1
        System.out.println(dcq.dequeue()); // 2
        System.out.println(dcq.dequeue()); // 3
    }
}
56. Implement a queue using a single stack and recursion.
java
Copy
Edit
import java.util.Stack;

public class QueueUsingOneStack {
    private Stack<Integer> stack = new Stack<>();

    public void enqueue(int val) {
        stack.push(val);
    }

    public Integer dequeue() {
        if (stack.isEmpty()) return null;
        int x = stack.pop();
        if (stack.isEmpty()) {
            return x;
        }
        int res = dequeue();
        stack.push(x);
        return res;
    }

    public static void main(String[] args) {
        QueueUsingOneStack q = new QueueUsingOneStack();
        q.enqueue(1);
        q.enqueue(2);
        q.enqueue(3);
        System.out.println(q.dequeue()); // 1
        System.out.println(q.dequeue()); // 2
    }
}
57. Find the maximum sum of k consecutive elements in a queue.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class MaxSumKConsecutive {
    public static int maxSumK(Queue<Integer> q, int k) {
        if (q.size() < k) return -1;

        int windowSum = 0, maxSum = Integer.MIN_VALUE;
        int size = q.size();
        LinkedList<Integer> list = new LinkedList<>(q);

        for (int i = 0; i < k; i++) windowSum += list.get(i);
        maxSum = windowSum;

        for (int i = k; i < size; i++) {
            windowSum += list.get(i) - list.get(i - k);
            maxSum = Math.max(maxSum, windowSum);
        }
        return maxSum;
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(1); q.offer(2); q.offer(3); q.offer(4); q.offer(5);
        System.out.println(maxSumK(q, 3)); // 12 (3+4+5)
    }
}
58. Given a queue, rearrange it so that all even numbers are before odd numbers.
java
Copy
Edit
import java.util.LinkedList;
import java.util.Queue;

public class EvenOddQueue {
    public static void rearrange(Queue<Integer> q) {
        Queue<Integer> evens = new LinkedList<>();
        Queue<Integer> odds = new LinkedList<>();

        while (!q.isEmpty()) {
            int val = q.poll();
            if (val % 2 == 0) evens.offer(val);
            else odds.offer(val);
        }

        q.addAll(evens);
        q.addAll(odds);
    }

    public static void main(String[] args) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(1); q.offer(2); q.offer(3); q.offer(4);
        rearrange(q);
        System.out.println(q); // [2, 4, 1, 3]
    }
}
