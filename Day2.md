## STACK using array


```java
public interface StackInterface<T> {
	void push(T element) throws stackexception;
	T pop()throws stackexception;
	T peek() throws stackexception;
	boolean isEmpty();
	int size();
	boolean isFull();
}
```

```java
public class stackexception extends Exception {
    public stackexception(String message) {
        super(message);
    }
}
```

```java

public class stackImpl<T> implements StackInterface<T> {
	private T[] array;
	private int size;
	private int top;

	@SuppressWarnings("unchecked")
	public stackImpl() {
		size = 10;
		array = (T[]) new Object[size];
		top = -1;
	}

	@Override
	public void push(T element) throws stackexception {
		if (!isFull()) {
			array[++top] = element;
		} else {
			growStack();
			array[++top] =  element;
		}
	}

	@Override
	public T pop() throws stackexception {
		if (!isEmpty()) {
			return array[top--];
		} else {
			throw new stackexception("Stack is empty");
		}
	}

	@Override
	public T peek() throws stackexception {
		if (!isEmpty()) {
			return array[top];
		} else {
			throw new stackexception("Stack is empty");
		}
	}

	@Override
	public boolean isEmpty() {
		if (top == -1) {
			return true;
		}
		return false;
	}

	@Override
	public int size() {
		return top + 1;
	}

	@Override
	public boolean isFull() {
		if (top == size - 1)
			return true;
		return false;
	}

	private void growStack() {
		int new_size = size * 2;
		@SuppressWarnings("unchecked")
		T[] newArray = (T[]) new Object[new_size];
		for (int i = 0; i < top; i++) {
			newArray[i] = array[i];
		}
		array = newArray;
		size = new_size;
	}
}
```

```java
import java.util.Scanner;
public class Main {
	public static void main(String[] args) {
		stackImpl<Integer> mystack = new stackImpl<Integer>();
		try(Scanner sc = new Scanner(System.in);){			
			mystack.push(10);
			mystack.push(20);
			mystack.push(10);
			mystack.push(20);
			mystack.push(10);
			mystack.push(20);
			System.out.println(mystack.pop());
		}catch(Exception e) {
			System.out.println(e.getMessage());
		}
	}

}
```

## Queue 


```java
public interface QueueInterface<T> {
	boolean add(T element) throws QueueException;
	boolean offer(T element);
	T element()throws QueueException;
	T peek();
	T remove() throws QueueException;
	T poll();
}
```

```java

public class QueueImpl<T> implements QueueInterface<T> {
	private T[]Array;
	private int size;
	private int front;
	private int rear;
	
	@SuppressWarnings("unchecked")
	public QueueImpl() {
		size = 20;
		front = -1;
		rear = -1;
		Array = (T[]) new Object[size];
	}
	@Override
	public boolean add(T element) throws QueueException {
		if(!isFull()) {
			if(front==-1)front=0;
			Array[++rear] = element;
			return true;
		}
		throw new QueueException("Error Adding Element");
	}

	@Override
	public boolean offer(T element) {
		if(!isFull()) {
			if(front==-1)front++;
			Array[++rear] = element;
			return true;
		}
		return false;
	}

	@Override
	public T element() throws QueueException {
		if(!isEmpty()) {
			return Array[front];
		}
		throw new QueueException("Queue is empty");
	}

	@Override
	public T peek() {
		if(!isEmpty()) {
			return Array[front];
		}
		return null;
	}

	@Override
	public T remove() throws QueueException {
		if(!isEmpty()) {
			T removedElement = Array[front];
            if (front >= rear) { // Queue is now empty
                front = -1;
                rear = -1;
            } else {
                front++;
            }
            return removedElement;
		}
		throw new QueueException("Queue is empty");
	}

	@Override
	public T poll() {
		if(!isEmpty()) {
			T removedElement = Array[front];
            if (front >= rear) { // Queue is now empty
                front = -1;
                rear = -1;
            } else {
                front++;
            }
            return removedElement;
		}
		return null;
	}
	
	private boolean isEmpty() {
		if(front == -1 ||front > rear) return true;
		return false;
	}
	private boolean isFull() {
		if(rear == size-1) {
			return true;
		}
		return false;
	}
}

```

```java
public class QueueException extends Exception{
	public QueueException(String message) {
		super(message);
	}
}
```

```java
interface Queue<T> {
    void enqueue(T item);
    T dequeue();
    T peek();
    boolean isEmpty();
    int size();
	void display();
}
```

```java
class LinkedList<T> {
    private Node<T> head;
    private int size;

    private static class Node<T> {
        T data;
        Node<T> next;

        Node(T data) {
            this.data = data;
            this.next = null;
        }
    }
    
    public LinkedList() {
    	this.size = 0;
    	this.head = null;
    }
    // LinkedList methods
    void add(T item) {
    	Node<T> node = new Node<T>(item);
    	if(head==null) {
    		head = node;
    	}else {
    		Node<T> temp = head;
    		while(temp.next!=null) {
    			temp = temp.next;
    		}
    		temp.next = node;
    	}
    	size++;
    }

    T remove() {
    	if (head == null) {
            throw new IllegalStateException("List is empty");
        }
        T data = head.data;
        head = head.next;
        size--;
        return data;
    }

    T getFirst() {
    	if (head == null) {
            throw new IllegalStateException("List is empty");
        }
        return head.data;
    }

    boolean isEmpty() {
    	return size==0;
    }
    public void display() {
        Node<T> current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }
	public int size() {
		return size;
	}
}
```

```java
public class QueueUsingLinkedList<T> implements Queue<T> {
    private LinkedList<T> list;

    public QueueUsingLinkedList() {
        list = new LinkedList<>();
    }

    @Override
    public void enqueue(T item) {
        list.add(item);
    }

    @Override
    public T dequeue() {
        return list.remove();
    }

    @Override
    public T peek() {
        return list.getFirst();
    }

    @Override
    public boolean isEmpty() {
        return list.isEmpty();
    }

    @Override
    public int size() {
        return list.size();
    }
    public void display() {
    	list.display();
    }
}
```

```java
import java.util.Scanner;
public class Main {
	public static void main(String[]args) {
		QueueImpl<Integer> queue= new QueueImpl<Integer>();
		try(Scanner sc = new Scanner(System.in)){
//			System.out.println("Testing add method:");
//            for (int i = 0; i < 20; i++) {
//                queue.add(i);
//            }
//
//            System.out.println("Testing add method when queue is full:");
//            try {
//                queue.add(21);
//            } catch (QueueException e) {
//                System.out.println(e.getMessage());
//            }
//
//            System.out.println("Testing offer method:");
//            System.out.println(queue.offer(21)); // Should print false because the queue is full
//
//            System.out.println("Testing element method:");
//            System.out.println(queue.element()); // Should print 0
//
//            System.out.println("Testing peek method:");
//            System.out.println(queue.peek()); // Should print 0
//
//            System.out.println("Testing remove method:");
//            for (int i = 0; i < 10; i++) {
//                System.out.println(queue.remove());
//            }
//
//            System.out.println("Testing poll method:");
//            for (int i = 0; i < 10; i++) {
//                System.out.println(queue.poll());
//            }
//
//            System.out.println("Testing remove method when queue is empty:");
//            try {
//                queue.remove();
//            } catch (QueueException e) {
//                System.out.println(e.getMessage());
//            }
//
//            System.out.println("Testing poll method when queue is empty:");
//            System.out.println(queue.poll()); // Should print null
	        Queue<Integer> queue1 = new QueueUsingLinkedList<>();
	        queue1.enqueue(1);
	        queue1.enqueue(2);
//	        System.out.println(queue1.dequeue()); // Output: 1
//	        System.out.println(queue1.peek());   // Output: 2
//	        System.out.println(queue1.isEmpty()); // Output: false
//	        System.out.println(queue1.size());    // Output: 1
			queue1.display();
		}catch(Exception e) {
			System.out.println(e.getMessage());
		}
	}
}
```
