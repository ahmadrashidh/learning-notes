# Tree

There are various types of Tree. One of the simplest is Binary Tree where there will 0 to 2 children under a node.


## Tree Node Object

```java
class TreeNode {
    int value; // can be of any datatype
    TreeNode left;
    TreeNode right;


    TreeNode(int data){
        this.value = data;
        this.left = null;
        this.right = null;
    }
}

TreeNode t = new TreeNode(12); // [null]<-[12]->[null]
t.left = new TreeNode(15); // [15]<-[12]->[null]
t.right = new TreeNode(17); // [15]<-[12]->[17]

```

- Every child of Tree is also Tree known as SubTree. 
- So this also shows that Tree DataStructure recursive in nature.

## Traversing a Tree

**Preorder**:Root Value, Left SubTree, Right SubTree
**Inorder**:Left SubTree, Root Value, Right SubTree
**Postorder**:Left SubTree, Right SubTree, Root Value


### Pre-order Traversal

```java
void preorder(root){
    if(root == null)
        return;

    System.out.println(root.value);
    preorder(root.left);
    preorder(root.right);
}
```

### In-order Traversal

```java
void inorder(root){


    if(root == null)
        return;

    inorder(root.left);

    System.out.println(root.value);
   
    inorder(root.right);
}
```

### Post-order Traversal

```java
void postorder(root){


    if(root == null)
        return;

    postorder(root.left);

    postorder(root.right);

    System.out.println(root.value);
}
```

Space Complexity of Tree problems are based on how many in `Call Stack`.

## Problems

Given 2 Trees. Return true if Trees are identical.

```java
boolean isTreeIdentical(TreeNode rootOne, TreeNode rootTwo){
    if(rootOne == null && rootTwo == null) return true;
    if(rootOne == null || rootTwo == null) return false;

    if(rootOne.value != rootTwo.value)
        return false;
    
    return (isTreeIdentical(rootOne.left, rootTwo.left) && isTreeIdentical(rootOne.right, rootTwo.right))
    
}
```

------

Given a Binary Tree. Return the height of the Tree.

**Height of the Tree**: Count of the nodes in the longest path from the root to the leaf.

i.e. maximum between height of left sub tree and height of right sub tree.

```java
int height(root){
    if(root == null) return 0;

    return 1 + Math.max(height(root.left), height(root.right));

}
```

TC:O(N)
SC:O(N)

