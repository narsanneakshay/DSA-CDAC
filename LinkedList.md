#### Interface
```java
public interface LinkedList<T> {
	void add(T element);
	void delete(T element);
	T search(T element);
	void display();
	void addSorted(T element);
}
```

#### Node Class
```java
public class Node<T extends Comparable<T>> {
	T data;
	public Node<T> next;
	
	public Node() {
		this.data = null;
		this.next = null;
	}

	public Node(T element) {
		this.data = element;
		this.next = null;
	}
}
```


#### Implementation class
```java
public class LinkedListImpl<T extends Comparable<T>> implements LinkedList<T>{
	private Node<T> head;
	
	public LinkedListImpl() {
		this.setHead(null);
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
	@Override
	public void delete(T element) {
		if(head == null) return;
		Node temp = head;
		Node Prev = head;
		while(temp.data !=element) {
			Prev = temp;
			temp=temp.next;
		}
		Prev.next= temp.next.next;
	}

	@Override
	public T search(T element) {
		if(head == null) return null;
		Node temp = head;
		while(temp!=null && temp.data.equals(element)) {
			temp = temp.next;
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
	public Node<T> getHead() {
		return head;
	}
	public void setHead(Node<T> head) {
		this.head = head;
	}

}
```

#### Main
```java

public class Main {

	public static void main(String[] args) {
		LinkedList<Integer> mylist = new LinkedListImpl();
		mylist.addSorted(10);
		mylist.addSorted(10);
		mylist.addSorted(20);
		mylist.delete(10);
		mylist.display();
	}

}
```
