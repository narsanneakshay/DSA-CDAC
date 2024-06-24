#### Inteface
```java
public interface DoublyLinkedList<T> {
	void add(T element);
	void delete(T element);
	T search(T element);
	void display();
	void addSorted(T element);
}
```
#### Node class
```java
public class Node<T extends Comparable<T>> {
	public Node<T>prev;
	T data;
	public Node<T> next;
	
	public Node() {
		this.prev = null;
		this.data = null;
		this.next = null;
	}

	public Node(T element) {
		this.prev = null;
		this.data = element;
		this.next = null;
	}
}
```

#### Implementation class
```java
public class DoublyLinkedImpl<T extends Comparable<T>> implements DoublyLinkedList<T> {
	private Node<T>head;
	public DoublyLinkedImpl() {
		this.head = null;
	}
	
	public DoublyLinkedImpl(Node<T> node) {
		this.head = node;
	}
	@Override
	public void add(T element) {
		if(head == null) {
			head = new Node<T>(element);
		}else {
			Node temp = head;
			while(temp.next!=null) {
				temp =temp.next;
			}
			temp.next = new Node<T> (element);
		}
	}

	@Override
	public void delete(T element) {
		if(head == null) return;
		Node temp = head;
		while(temp!=null &&  !temp.data.equals(element)) {
			temp=temp.next;
		}
	    if (temp == null) {
	        System.out.println("Element not found");
	        return;
	    }
	    if (temp.prev != null) {
	        temp.prev.next = temp.next;
	    } else {
	        head = temp.next;
	        if (head != null) {
	            head.prev = null;
	        }
	    }
	    if (temp.next != null) {
	        temp.next.prev = temp.prev;
	    }
	}

	@Override
	public T search(T element) {
		if(head == null) return null;
		Node temp = head;
		while(temp!=null && (element.compareTo((T) temp.data) != 0 )) {
			temp = temp.next;
		}
		if(temp !=null) {
			return (T) temp.data;
		}
		return null;
	}

	@Override
	public void display() {
		Node temp = head;
		while(temp!=null) {
			System.out.println(temp.data);
			temp = temp.next;
		}
	}

	@Override
	public void addSorted(T element) {
		if(head == null) {
			head = new Node<T>(element);
		}else {
			Node temp = head;
			Node prev = null;
			while(temp!=null && element.compareTo((T) temp.data) > 0 ) {
				prev = temp;
				temp =temp.next;
			}
			Node<T> newNode = new Node<T>(element);
	        
	        if(prev == null) {
	            newNode.next = head;
	            head = newNode;
	        } else {
	            prev.next = newNode;
	            newNode.next = temp;
	        }
		}
	}

}
```

#### Main
```java

public class Main {

	public static void main(String[] args) {
		DoublyLinkedList<Integer> mylist = new DoublyLinkedImpl();
		mylist.addSorted(10);
		mylist.addSorted(10);
		mylist.addSorted(20);
		mylist.delete(20);
		mylist.display();
	}
}
```
