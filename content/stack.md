## 栈

在栈(stack)中，被删除的是最近插入的元素：栈实现的是一种后进先出(last-in, first-out, LIFO)策略。

栈上的插入操作称为压入(push)，而无元素参数的删除操作称为弹出(pop)。这两个名字使人联想到现实中的栈，比如餐馆里装有弹簧的摞盘子的栈。盘子从栈中弹出的次序刚好同它们被压入的次序相反，这是因为只有最上面的盘子才能被取下来。

可以用一个数组arr[0...n-1]来实现一个最多可容纳n个元素的栈。该数组有一个属性top，指向最新插入的元素。栈中包含的元素为arr[0...top]，其中arr[0]是栈底元素，arr[top]是栈顶元素。当top = 0时，栈中不包含任何元素，即栈是空的。当top = n - 1时，栈是满的。

```java
public class Stack {
    private int top;
    private int[] keys;
    
    public Stack(int capacity) {
        top = -1;
        keys = new int[capacity];
    }
    
    public boolean isEmpty() {
        return top == -1;
    }
    
    public boolean isFull() {
        return top == keys.length - 1;
    }
    
    public void push(int key) {
        if (isFull()) {
            throw new RuntimeException("stack overflow");
        }
        keys[++top] = key;
    }
    
    public int pop() {
        if (isEmpty()) {
            throw new RuntimeException("stack underflow");
        }
        return keys[top--];
    }
}
```
