# Week 7 - Search trees

# Binary Search Tree BST

A binary search tree (BST) is a type of data structure that allows for efficient insertion, deletion, and search operations. It is called a "binary" tree because each node has at most two children, and it is called a "search" tree because it can be used to search for a specific element in the tree.

In a BST, each node stores an element and has a left child and a right child. The left child of a node contains elements that are smaller than the element stored in the node, while the right child contains elements that are larger. This property is known as the "BST property".

The basic operations that can be performed on a BST include:

- Insertion: Adding a new element to the tree.
- Deletion: Removing an element from the tree.
- Search: Finding an element in the tree.
- In-order traversal: Visiting each node in the tree in ascending order of the element stored in the node.
- Pre-order traversal: Visiting each node in the tree in the order of the root, left child, right child.
- Post-order traversal: Visiting each node in the tree in the order of the left child, right child, root.

In Java, a BST can be implemented using a class that represents a node in the tree. The class should have instance variables for the element stored in the node, the left child, and the right child. The class should also have methods for the basic operations of insertion, deletion, and search.

```java
class Node {
    int key;
    Node left, right;
 
    public Node(int item) {
        key = item;
        left = right = null;
    }
}
 
class BST {
    Node root;
 
    BST() { 
        root = null; 
    }
 
    void insert(int key) {
       root = insertRec(root, key);
    }
     
    Node insertRec(Node root, int key) {
 
        if (root == null) {
            root = new Node(key);
            return root;
        }
 
        if (key < root.key)
            root.left = insertRec(root.left, key);
        else if (key > root.key)
            root.right = insertRec(root.right, key);
 
        return root;
    }

/**This function accepts the root of the BST and the key of the node that needs to be deleted. It first checks if the root is null, in which case it returns the root. 
If the key is less than the root's key, the function recursively calls itself on the left child. If the key is greater than the root's key, the function recursively calls itself on the right child.

If the key is equal to the root's key, the function checks if the root has no left child or no right child. If it has no left child, it returns the right child and vice versa.

Otherwise, the function finds the inorder successor of the root and replace the root with the inorder successor. Then the function recursively calls itself to delete the inorder successor.

You need to have a helper function minValue(Node root) which gives the minimum value in right subtree of the node.
*/

Node deleteNode(Node root, int key) {
        if (root == null)  return root;
 
        if (key < root.key)
            root.left = deleteNode(root.left, key);
 
        else if (key > root.key)
            root.right = deleteNode(root.right, key);
 
        else {
            if (root.left == null)
                return root.right;
            else if (root.right == null)
                return root.left;
 
            root.key = minValue(root.right);
 
            root.right = deleteNode(root.right, root.key);
        }
 
        return root;
    }

/**
This function finds the minimum value in the right subtree of the node and returns it. This value is used to replace the node that is being deleted.
It would be great if you could use this function with the main class you have for BST.
*/

int minValue(Node root) {
        int minv = root.key;
        while (root.left != null) {
            minv = root.left.key;
            root = root.left;
        }
        return minv;
    }
 
    void inorder()  {
       inorderRec(root);
    }
 
    void inorderRec(Node root) {
        if (root != null) {
            inorderRec(root.left);
            System.out.println(root.key);
            inorderRec(root.right);
        }

boolean search(Node root, int key) {
        if (root == null)
            return false;
 
        if (root.key == key)
            return true;
 
        if (root.key > key)
            return search(root.left, key);
 
        return search(root.right, key);
    }

    }
 
    public static void main(String[] args) {
        BST tree = new BST();
 
        tree.insert(50);
        tree.insert(30);
        tree.insert(20);
        tree.insert(40);
        tree.insert(70);
        tree.insert(60);
        tree.insert(80);
 
        tree.inorder();
    }
}
```

![Untitled](Untitled%2015.png)

![Untitled](Untitled%2016.png)

# AVL tree

  An AVL tree is a self-balancing binary search tree, where the difference between the heights of the left and right subtrees cannot be more than one. The AVL tree is named after its two Soviet inventors, G.M. Adelson-Velsky and E.M. Landis. 

It has the same operations as a normal BST, but now we must assure the balance property is kept. To keep the AVL tree property, we must do rotations when the difference between the heights of 2 subtrees is more than 1.

To maintain the balance property, AVL trees use a technique called rotation. There are two types of rotations:

- Left rotation: The left subtree becomes the new root, and the original root becomes the right child of the new root.
- Right rotation: The right subtree becomes the new root, and the original root becomes the left child of the new root.
    
    ### Insertion example in AVL tree:
    
    1. Insert the element into the tree as in a standard binary search tree.
    2. Check the balance factor of the current node. The balance factor is the difference between the height of the left subtree and the height of the right subtree.
    3. If the balance factor is greater than 1, it means the left subtree is heavier. In this case, check the balance factor of the left child.
        - If the balance factor of the left child is greater than or equal to 0, perform a right rotation on the current node.
        - If the balance factor of the left child is less than 0, perform a left rotation on the left child, then a right rotation on the current node.
    4. If the balance factor is less than -1, it means the right subtree is heavier. In this case, check the balance factor of the right child.
        - If the balance factor of the right child is less than or equal to 0, perform a left rotation on the current node.
        - If the balance factor of the right child is greater than 0, perform a right rotation on the right child, then a left rotation on the current node.
    5. Repeat steps 2-4 for all ancestors of the current node.

### Rotations

Left Rotation: The left rotation operation is performed when the balance factor of a node is greater than 1 and the balance factor of its left child is greater than or equal to 0.
In a left rotation, the left subtree of the unbalanced node becomes the new root and the current root node becomes the right child of the new root.
This operation helps in reducing the height of the left subtree and rebalancing the tree.

In simple terms, rotation is a way of moving the nodes around in the tree to balance it and make sure the difference in height between left and right subtree is not too big. This allows us to maintain the balance property of the tree, and keep the time complexity of operations like search, insertion and deletion to be O(log n)

```java
class Node {
    int key, height;
    Node left, right;
 
    Node(int d) {
        key = d;
        height = 1;
    }
}
 
class AVLTree {
 
    Node root;
 
    int height(Node N) {
        if (N == null)
            return 0;
 
        return N.height;
    }
 
    int max(int a, int b) {
        return (a > b) ? a : b;
    }
 
    Node rightRotate(Node y) {
        Node x = y.left;
        Node T2 = x.right;
 
        x.right = y;
        y.left = T2;
 
        y.height = max(height(y.left), height(y.right)) + 1;
        x.height = max(height(x.left), height(x.right)) + 1;
 
        return x;
    }
 
    Node leftRotate(Node x) {
        Node y = x.right;
        Node T2 = y.left;
 
        y.left = x;
        x.right = T2;
 
        x.height = max(height(x.left), height(x.right)) + 1;
        y.height = max(height(y.left), height(y.right)) + 1;
 
        return y;
    }
 
    int getBalance(Node N) {
        if (N == null)
            return 0;
 
        return height(N.left) - height(N.right);
    }
 
    Node insert(Node node, int key) {
 
        if (node == null)
            return (new Node(key));
 
        if (key < node.key)
            node.left = insert(node.left, key);
        else if (key > node.key)
            node.right = insert(node.right, key);
        else
            return node;
 
        node.height = 1 + max(height(node.left),
                              height(node.right));
 
        int balance = getBalance(node);
 
        if (balance > 1 && key < node.left.key)
            return rightRotate(node);
 
        if (balance < -1 && key > node.right.key)
            return leftRotate(node);
 
        if (balance > 1 && key > node.left.key) {
            node.left = leftRotate(node.left);
            return rightRotate(node);
        }
 
        if (balance < -1 && key < node.right.key) {
            node.right = rightRotate(node.right);
            return leftRotate(node);
        }
 
        return node;
    }
 
    void preOrder(Node node) {
if (node != null) {
System.out.print(node.key + " ");
preOrder(node.left);
preOrder(node.right);
}
}
 
Node minValueNode(Node node) {
    Node current = node;

    while (current.left != null)
        current = current.left;

    return current;
}

Node deleteNode(Node root, int key) {

    if (root == null)
        return root;

    if (key < root.key)
        root.left = deleteNode(root.left, key);

    else if (key > root.key)
        root.right = deleteNode(root.right, key);

    else {
        if ((root.left == null) || (root.right == null)) {
            Node temp = null;
            if (temp == root.left)
                temp = root.right;
            else
                temp = root.left;

            if (temp == null) {
                temp = root;
                root = null;
            } else
                root = temp;
        } else {
            Node temp = minValueNode(root.right);
            root.key = temp.key;
            root.right = deleteNode(root.right, temp.key);
        }
    }

    if (root == null)
        return root;

    root.height = max(height(root.left), height(root.right)) + 1;

    int balance = getBalance(root);

    if (balance > 1 && getBalance(root.left) >= 0)
        return rightRotate(root);

    if (balance > 1 && getBalance(root.left) < 0) {
        root.left = leftRotate(root.left);
        return rightRotate(root);
    }

    if (balance < -1 && getBalance(root.right) <= 0)
        return leftRotate(root);

    if (balance < -1 && getBalance(root.right) > 0) {
        root.right = rightRotate(root.right);
        return leftRotate(root);
    }

    return root;
}

boolean search(Node root, int key) {
    if (root == null)
        return false;

    if (root.key == key)
        return true;

    if (root.key > key)
        return search(root.left, key);

    return search(root.right, key);
}
```

```java
			 x                             y
      / \                           / \
     a   y    left rotate on x     x   c
        / \   ---------------->   / \
       b   c                     a   b
```

![Untitled](Untitled%2017.png)

Insertion in AVL tree is a process of adding a new element to the tree while maintaining the balance property of the tree. The basic steps for insertion are as follows:

1. Starting at the root, navigate through the tree like a regular binary search tree to find the correct position for the new element.
2. Insert the new element in the empty position.
3. Check the balance factor of each node, if the balance factor is greater than 1 or less than -1, rotate the tree to balance it.
4. Repeat steps 3-4 for all ancestors of the current node.
5. Update the height of each node affected by the insertion and rotation operations.

In simple terms, insertion in AVL tree is just like adding a new element in a regular binary search tree, but with the additional step of balancing the tree to keep it organized and maintain the time complexity of the operations.

Deletion in AVL tree is a process of removing an element from the tree while maintaining the balance property of the tree. The basic steps for deletion are as follows:

1. Starting at the root, navigate through the tree like a regular binary search tree to find the element to be deleted.
2. Once the element to be deleted is found, if it has no children, simply remove it. If it has one child, remove it and replace it with its child. If it has two children, find the next smallest element in the tree, replace the element to be deleted with it and remove the next smallest element from its original position.
3. Check the balance factor of each node, if the balance factor is greater than 1 or less than -1, rotate the tree to balance it.
4. Repeat steps 3-4 for all ancestors of the current node.
5. Update the height of each node affected by the deletion and rotation operations.

In simple terms, deletion in AVL tree is just like removing an element in a regular binary search tree, but with the additional step of balancing the tree to keep it organized and maintain the time complexity of the operations.

![Untitled](Untitled%2018.png)

# (2, 4) Tree

A 2-4 tree is a type of balanced search tree that allows for up to three data elements per node (hence the name "2-4" tree). Each node in a 2-4 tree can have either two or four children, and the tree is structured such that the height of the tree is kept as small as possible.

The basic operations that can be performed on a 2-4 tree include:

- Insertion: Adding a new element to the tree while maintaining the balance property.
- Deletion: Removing an element from the tree while maintaining the balance property.
- Search: Finding an element in the tree.

### Insert

Here is the basic procedure for inserting a new element into a 2-4 tree:

1. Starting at the root of the tree, navigate to the leaf node where the new element belongs.
2. If the leaf node has less than 3 elements, insert the new element in its proper place.
3. If the leaf node has 3 elements, split it into two nodes and move the middle element to its parent node.
4. Repeat step 3 for all ancestors of the current node until the root node is reached.
5. If the root node has 4 elements, split it into two nodes and create a new root node with the middle element.

The basic procedure for deletion is similar to insertion, but with additional steps to handle the case when a node has only one element after deletion.

2-4 trees have the advantage of keeping the height of the tree relatively small, and providing an efficient way of searching, insertion and deletion, with a time complexity of O(log n)
It is important to note that, 2-4 Trees is not a widely used data structure, but it has some similarities with B-Trees which are widely used in databases and file systems.

### Delete

1. Starting at the root of the tree, navigate to the leaf node where the element to be deleted is located.
2. If the leaf node has more than 2 elements, simply remove the element from the node and sort the remaining elements.
3. If the leaf node has only 2 elements, check if any of its siblings has more than 2 elements. If so, borrow an element from a sibling and move it to the current node.
4. If all siblings have only 2 elements, merge the current node with one of its siblings and move the middle element to its parent node.
5. Repeat steps 3 and 4 for all ancestors of the current node until the root node is reached.
6. If the root node has only 1 element, and it is the element being deleted, set the only child as the new root of the tree.
7. If the root node has only 1 element, and it is not the element being deleted, adjust the tree as necessary.
8. For each node that is underfull, check if any of its siblings has more than 2 elements. If so, borrow an element from a sibling and move it to the current node.
9. If all siblings have only 2 elements, merge the current node with one of its siblings and move the middle element to its parent node.
10. Repeat steps 8 and 9 for all ancestors of the current node until the root node is reached.

The time complexity of the deletion operation in a 2-4 tree is O(log n) because it needs to go down the path of the tree to find the element and remove it, where log n is the height of the tree.

### Operations only it has:

1. Split: This operation is used when a node becomes full, meaning it contains the maximum number of elements it can hold (in the case of 2-4 Trees, 3 elements). When a node is full, it must be split into two separate nodes to make room for new elements and maintain the balance of the tree.
2. Merge: This operation is used when a node becomes underfull, meaning it contains less than the minimum number of elements it can hold (in the case of 2-4 Trees, 2 elements). When a node is underfull, it may be merged with another node to make the tree more balanced.
3. Rotation: This operation is used to maintain the balance of the tree when a node becomes unbalanced. Rotations are used to move elements between nodes to make the tree more balanced.
4. Rebalancing: 2-4 Trees uses these operations (split, merge, and rotation) to keep the tree balanced, which is done recursively. The tree is checked for balance after each insertion and deletion operation, and if it is found to be unbalanced, the tree is rebalanced.

The split operation is used in 2-4 Trees when a node becomes full, meaning it contains the maximum number of elements it can hold (in this case, 3 elements). When a node is full, it must be split into two separate nodes in order to maintain the balance of the tree and make room for new elements.

The basic steps for the split operation are:

1. Create a new node, called 'newNode', with the same properties as the node being split.
2. Move the middle element of the full node to the parent node. This element becomes the key that separates the two new nodes.
3. Move the elements on the right side of the middle element to the newNode.
4. Move the children on the right side of the middle element to the newNode.
5. Adjust the number of elements in the original node and the newNode.
6. Add the newNode as a child of the parent node.
7. Repeat this process for all ancestors of the current node until the root node is reached. If the root node becomes full, it is also split and a new root node is created with the middle element.

The split operation ensures that the 2-4 tree remains balanced and that the height of the tree is kept as small as possible. It's important to note that split operation can be applied recursively on the parent of the node until the root node. This will increase the height of the tree by 1, but it ensures that the tree remains balanced.

The time complexity of the split operation is O(log n) because it needs to go up the path of the tree and update the nodes on the way, where log n is the height of the tree.

# Red Black Tree

A Red-Black Tree is a type of self-balancing binary search tree that is used to maintain a data structure with a logarithmic time complexity for the basic operations (search, insertion, and deletion). The basic idea behind a Red-Black Tree is to color each node of the tree either red or black in such a way that the tree remains balanced.

In a Red-Black Tree, each node has a color attribute that can have one of two values: red or black. The root node is always black and the leaves are represented by a special type of node called NIL, which are also colored black.

The main rules that Red-Black Trees follow to maintain their balance are:

1. A node is either red or black.
2. The root is black.
3. All leaves (NIL) are black.
4. Every red node must have two black child nodes.
5. Every path from a node to any of its descendant NIL nodes must contain the same number of black nodes.

When a new node is inserted into a Red-Black Tree, it is first inserted as if it were a regular binary search tree. Then the tree is checked for violations of the red-black tree rules, if any violation is found, the tree is rotated and/or recolored to fix it.

Similarly, when a node is deleted from a Red-Black Tree, it is first deleted as if it were a regular binary search tree. Then the tree is checked for violations of the red-black tree rules, if any violation is found, the tree is rotated and/or recolored to fix it.

The time complexity of the basic operations (search, insertion, and deletion) in a Red-Black Tree is O(log n) in the average case, and O(n) in the worst case.

It is important to note that, Red-Black Trees is a widely used data structure, it's used in various libraries such as Java's TreeMap and TreeSet.

```java
class RedBlackTree {
    private static final boolean RED = true;
    private static final boolean BLACK = false;
 
    class Node {
        int data;
        Node left, right;
        boolean color;
 
        Node(int data) {
            this.data = data;
            color = RED;
        }
    }
 
    private boolean isRed(Node x) {
        if (x == null) return false;
        return x.color == RED;
    }
 
    private Node rotateLeft(Node h) {
        Node x = h.right;
        h.right = x.left;
        x.left = h;
        x.color = h.color;
        h.color = RED;
        return x;
    }
 
    private Node rotateRight(Node h) {
        Node x = h.left;
        h.left = x.right;
        x.right = h;
        x.color = h.color;
        h.color = RED;
        return x;
    }
 
    private void flipColors(Node h) {
        h.color = !h.color;
        h.left.color = !h.left.color;
        h.right.color = !h.right.color;
    }
 
    public Node insert(Node h, int data) {
        if (h == null) return new Node(data);
 
        if (data < h.data) h.left = insert(h.left, data);
        else if (data > h.data) h.right = insert(h.right, data);
 
        if (isRed(h.right) && !isRed(h.left)) h = rotateLeft(h);
        if (isRed(h.left) && isRed(h.left.left)) h = rotateRight(h);
        if (isRed(h.left) && isRed(h.right)) flipColors(h);
 
        return h;
    }
}
```

Here is an explanation of the logic behind the main methods used in the example code:

1. **`rotateLeft(Node h)`**: This method is used when a right-leaning red link is found. The method rotates the link to the left and flips the colors of the link and its child to maintain the balance of the tree.
2. **`rotateRight(Node h)`**: This method is used when a left-leaning red link and a left-leaning red link of its child is found. The method rotates the link to the right and flips the colors of the link and its child to maintain the balance of the tree.
3. **`flipColors(Node h)`**: This method is used when a red link and both of its children are red. The method flips the colors of the link and its children to maintain the balance of the tree.
4. **`insert(Node h, int data)`**: This method is used to insert a new node into the tree. It first checks whether the new node should be inserted to the left or the right of the current node, and then it checks for any violations of the red-black tree rules, and if any violation is found it applies the necessary rotations and color flips to fix it.

The idea behind these methods is to maintain the balance of the tree by ensuring that the tree follows the rules of Red-Black Trees. If a violation of these rules is found, the rotations and color flips are used to fix it and bring the tree back to a balanced state.

It's important to note that a Red-Black Tree is a balanced binary search tree, therefore, it guarantees a time complexity of O(log n) for search, insertion and deletion operations in average case, which is the same time complexity of AVL Trees and is better than the time complexity of unbalanced search trees like Simple Binary Search Tree which is O(n)

### Complexities

The time complexity of the basic operations (search, insertion, and deletion) in a Red-Black Tree is O(log n) in the average case, and O(n) in the worst case. This is because, in the average case, the height of a Red-Black Tree is O(log n), which means that the basic operations take O(log n) time, but in the worst case, the height of the tree can be O(n) which means that the basic operations take O(n) time.

The space complexity of a Red-Black Tree is O(n) because it stores all the elements in the tree, and each element takes a constant amount of space.

It's worth mentioning that the space complexity of a Red-Black Tree is the same as for a simple binary search tree.

It's important to note that, the time complexity of Red-Black Trees is guaranteed because it's a self-balancing tree, it's guaranteed that the tree will not become skewed, and the height of the tree will always be logarithmic to the number of elements in the tree.

# Helpful stuff

### Best method I ever came across to obtain the height of a tree or subtree (works on both).

```java
public static int height(BinaryTree tree) {
            if (tree == null) {
                return 0;
            }
            int leftHeight = height(tree.getLeft());
            int rightHeight = height(tree.getRight());
            return Math.max(leftHeight, rightHeight) + 1;
        }

```

### Method for determining if it has the order property

```java
public static boolean isTreeBst(BinaryTree tree, int min, int max) {
        if (tree == null) {
            return true;
        }

        if (tree.getKey() <= min || tree.getKey() >= max) {
            return false;
        }
        return (isTreeBst(tree.getLeft(), min, tree.getKey())) && 
																								(isTreeBst(tree.getRight(), tree.getKey(), max));
    }
```