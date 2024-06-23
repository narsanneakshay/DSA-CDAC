## Binary Tree

```java
public class Node<T extends Comparable<T>> {
    Node<T> left;
    T data;
    Node<T> right;

    Node(T data) {
        this.data = data;
        this.left = null;
        this.right = null;
    }
}
```

```java
public interface BinaryTree<T extends Comparable<T>> {
    void insert(T element) throws BinaryTreeException;
    void delete(T element) throws BinaryTreeException;
    void inorderTraversal() throws BinaryTreeException;
    void preorderTraversal() throws BinaryTreeException;
    void postorderTraversal() throws BinaryTreeException;
    T search(T element) throws BinaryTreeException;
    boolean isEmpty();
    int size();
}
```

```java

@SuppressWarnings("serial")
public class BinaryTreeException extends Exception {
	public BinaryTreeException(String message) {
		super(message);
	}
}
```

```java
public class BinaryTreeImpl<T extends Comparable<T>> implements BinaryTree<T> {
	private Node<T> root;
	private int size;

	public BinaryTreeImpl() {
		root = null;
		size = 0;
	}

	@Override
	public void insert(T element) throws BinaryTreeException {
		if (root == null) {
			root = new Node<>(element);
			size++;
		} else {
			insertElement(root, element);
		}
	}

	@Override
	public void delete(T element) throws BinaryTreeException {
		root = deleteElement(root, element);
	}

	@Override
	public void inorderTraversal() throws BinaryTreeException {
		inorderTraversal(root);
	}

	@Override
	public void preorderTraversal() throws BinaryTreeException {
		preorderTraversal(root);
	}

	@Override
	public void postorderTraversal() throws BinaryTreeException {
		postorderTraversal(root);
	}

	@Override
	public T search(T element) throws BinaryTreeException {
		return searchElement(root, element);
	}

	@Override
	public boolean isEmpty() {
		return root == null;
	}

	@Override
	public int size() {
		return size;
	}

	private void postorderTraversal(Node<T> node) throws BinaryTreeException {
		if (node != null) {
			postorderTraversal(node.left);
			postorderTraversal(node.right);
			System.out.print(node.data + " ");
		}
	}

	private void preorderTraversal(Node<T> node) throws BinaryTreeException {
		if (node != null) {
			System.out.print(node.data + " ");
			preorderTraversal(node.left);
			preorderTraversal(node.right);
		}
	}

	private void inorderTraversal(Node<T> node) throws BinaryTreeException {
		if (node != null) {
			inorderTraversal(node.left);
			System.out.print(node.data + " ");
			inorderTraversal(node.right);
		}
	}

	private T searchElement(Node<T> node, T element) throws BinaryTreeException {
		if (node == null) {
			throw new BinaryTreeException("Element not found in the tree");
		}
		if (element.equals(node.data)) {
			return node.data;
		} else if (element.compareTo(node.data) < 0) {
			return searchElement(node.left, element);
		} else {
			return searchElement(node.right, element);
		}
	}

	private Node<T> deleteElement(Node<T> node, T element) throws BinaryTreeException {
		if (node == null) {
			throw new BinaryTreeException("Element not found in the tree");
		}

		if (element.compareTo(node.data) < 0) {
			node.left = deleteElement(node.left, element);
		} else if (element.compareTo(node.data) > 0) {
			node.right = deleteElement(node.right, element);
		} else {
			if (node.left == null) {
				size--;
				return node.right;
			} else if (node.right == null) {
				size--;
				return node.left;
			}
			node.data = findMin(node.right).data;
			node.right = deleteElement(node.right, node.data);
		}

		return node;
	}

	private Node<T> findMin(Node<T> node) {
		while (node.left != null) {
			node = node.left;
		}
		return node;
	}

	private void insertElement(Node<T> node, T element) throws BinaryTreeException {
		if (element.equals(node.data)) {
			throw new BinaryTreeException("Element already exists in the tree");
		} else if (element.compareTo(node.data) < 0) {
			if (node.left == null) {
				node.left = new Node<>(element);
				size++;
			} else {
				insertElement(node.left, element);
			}
		} else {
			if (node.right == null) {
				node.right = new Node<>(element);
				size++;
			} else {
				insertElement(node.right, element);
			}
		}
	}

}
```

```java
public class Main {
    public static void main(String[] args) {
        BinaryTree<Integer> tree = new BinaryTreeImpl<>();
        try {
            tree.insert(5);
            tree.insert(3);
            tree.insert(7);
            tree.insert(2);
            tree.insert(4);
            tree.insert(6);
            tree.insert(8);
            tree.delete(5);
            System.out.print("In-order traversal of the tree: ");
            tree.inorderTraversal();
        } catch (BinaryTreeException e) {
            System.out.println(e.getMessage());
        }
    }
}
```
