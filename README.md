# Data-structure-program-06
 --- Binary Search Tree Operations ---
1. Insert
2. Search
3. Delete
4. Display (Inorder)
5. Exit
Enter your choice: 1
Enter value to insert: 50
Element inserted.

Enter your choice: 1
Enter value to insert: 30
Element inserted.

Enter your choice: 1
Enter value to insert: 70
Element inserted.

Enter your choice: 4
BST elements (Inorder):
30 50 70

Enter your choice: 2
Enter value to search: 30
Element found in BST.

Enter your choice: 3
Enter value to delete: 50
Element deleted (if present).
 # AVL Tree Insertion

class Node:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None
        self.height = 1

def height(n):
    return n.height if n else 0

def balance(n):
    return height(n.left) - height(n.right) if n else 0

def rightRotate(y):
    x = y.left
    y.left = x.right
    x.right = y
    y.height = 1 + max(height(y.left), height(y.right))
    x.height = 1 + max(height(x.left), height(x.right))
    return x

def leftRotate(x):
    y = x.right
    x.right = y.left
    y.left = x
    x.height = 1 + max(height(x.left), height(x.right))
    y.height = 1 + max(height(y.left), height(y.right))
    return y

def insert(root, key):
    if not root:
        return Node(key)
    if key < root.key:
        root.left = insert(root.left, key)
    else:
        root.right = insert(root.right, key)

    root.height = 1 + max(height(root.left), height(root.right))
    b = balance(root)

    if b > 1 and key < root.left.key:
        return rightRotate(root)
    if b < -1 and key > root.right.key:
        return leftRotate(root)
    return root

def inorder(root):
    if root:
        inorder(root.left)
        print(root.key, end=" ")
        inorder(root.right)

root = None
for i in [10, 20, 30, 40, 50]:
    root = insert(root, i)

print("AVL Tree Inorder Traversal:")
inorder(root)
