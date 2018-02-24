## 225. Implement Stack using Queues

Implement the following operations of a stack using queues.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
empty() -- Return whether the stack is empty.

**Notes:**

* You must use only standard operations of a queue -- which means only push to back, peek/pop from front, size, and is empty operations are valid.
* Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
* You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).

### 使用一个队列

```java
class MyStack {
    Queue<Integer> queue = new LinkedList<Integer>();
    int tail;
    /** Initialize your data structure here. */
    public MyStack() {
        
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        queue.add(x);
        for (int i = 1; i < queue.size(); i++) queue.add(queue.poll());
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        return queue.poll();
    }
    
    /** Get the top element. */
    public int top() {
        return queue.peek();
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return queue.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```

在push完之后反转一下队列，使最新加入的元素在最前

### 使用两个队列

```java
class MyStack {
    Queue<Integer> queue1 = new LinkedList<Integer>();
    Queue<Integer> queue2 = new LinkedList<Integer>();
    /** Initialize your data structure here. */
    public MyStack() {
        
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        
        if (queue1.isEmpty()) {
            queue1.add(x);
            for (int i = 0; i < queue2.size(); i++) queue1.add(queue2.poll());
        } else {
            queue2.add(x);
            for (int i = 0; i < queue1.size(); i++) queue2.add(queue1.poll());
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        if (queue1.isEmpty()) return queue2.poll();
        else return queue1.poll();
    }
    
    /** Get the top element. */
    public int top() {
        if (queue1.isEmpty()) return queue2.peek();
        else return queue1.peek();
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return queue1.isEmpty() && queue2.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```
使用两个队列，每次向一个空队列中push一个元素，将另一个队列中的元素加到当前队列的尾部。