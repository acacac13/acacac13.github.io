---
title: 二叉树
date: 2021-08-19 15:45:28
index_img: ../picture/20210819155025.png
banner_img: ../picture/20210819155025.png
tags: 
  - 树
  - 二叉树
categories: 数据结构与算法
---

# 简介

二叉树的特点是每个结点最多只能有两颗子树，且有左右之分。

> 定义：
>
> 二叉树（binary tree）是指树中节点的度不大于2的有序树，它是一种最简单且最重要的树。

一些类型：

* 满二叉树：只有度为0的结点和度为2的结点，并且度为0的结点在同一层上
* 完全二叉树：深度为k，有n个结点的二叉树当且仅当其每一个结点都与深度为k的满二叉树中编号从1到n的结点一一对应。

完全二叉树的特点：

1. 叶子结点只可能出现在层序最大的两层上
2. 某个结点的左分支下子孙的最大层序与右分支下子孙的最大层序相等或大1



# 遍历

二叉树有深度遍历和广度遍历，深度遍历有前序遍历，中序遍历，后序遍历三种遍历方法，广度遍历即层次遍历

> *注：二叉树的先序遍历才是严格按图的深度优先的算法，但是中序和后序也是深度优先，只是访问根结点的时机不同*

* 前序遍历：根结点 --> 左子树 --> 右子树
* 中序遍历：左子树 --> 根结点 --> 右子树
* 后序遍历：左子树 --> 右子树 --> 根结点
* 层序遍历：按层从左至右

## 前序遍历

### 递归

```java
/**
 * 前序遍历递归版本
 */
public void preOrderTraverse1(TreeNode root){
    if (root != null){
        System.out.print(root.val + " ");
        preOrderTraverse1(root.left);
        preOrderTraverse1(root.right);
    }
}
```

### 非递归

思路：

1. 先访问头结点，并把头节点入栈，当前节点置为左孩子
2. 判断节点是否为空，若为空，则取出栈顶结点并出栈，将右孩子置为当前结点；若不为空，则重复1直到当前结点为空或栈为空

```java
/**
 * 前序遍历非递归版本
 */
public void preOrderTraverse2(TreeNode root){
    LinkedList<TreeNode> stack = new LinkedList<>();
    TreeNode pNode = root;
    while (pNode != null || !stack.isEmpty()){
        if (pNode != null){
            System.out.print(pNode.val + " ");
            stack.push(pNode);
            pNode = pNode.left;
        } else {
            TreeNode node = stack.pop();
            pNode = node.right;
        }
    }
}

/**
 * 前序遍历非递归版本2
 */
public static void preOrderTraverse3(TreeNode root){
    if (root == null) {
        return;
    }
    LinkedList<TreeNode> stack = new LinkedList<>();
    stack.push(root);
    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        System.out.print(node.val + " ");
        if (node.right != null) {
            stack.push(node.right);
        }
        if (node.left != null) {
            stack.push(node.left);
        }
    }
}
```

## 中序遍历

### 递归

```java
/**
 * 中序遍历递归版本
 */
public void inOrderTraverse1(TreeNode root){
    if (root != null){
        inOrderTraverse1(root.left);
        System.out.print(root.val + " ");
        inOrderTraverse1(root.right);
    }
}
```

### 非递归

```java
/**
 * 中序遍历非递归版本
 */
public void inOrderTraverse2(TreeNode root){
    LinkedList<TreeNode> stack = new LinkedList<>();
    TreeNode pNode = root;
    while (pNode != null || !stack.isEmpty()){
        if (pNode != null){
            stack.push(pNode);
            pNode = pNode.left;
        } else {
            TreeNode node = stack.pop();
            System.out.print(node.val + " ");
            pNode = node.right;
        }
    }
}
```

## 后序遍历

### 递归

```java
/**
 * 后序遍历递归版本
 */
public void postOrderTraverse1(TreeNode root){
    if (root != null){
        postOrderTraverse1(root.left);
        postOrderTraverse1(root.right);
        System.out.print(root.val + " ");
    }
}
```

### 非递归

思路：需要用到两个栈，在节点不为空的情况下，依次将根节点、右儿子、左儿子压入一个栈stack2中，最后一起打印栈中的元素

```java
/**
 * 后序遍历非递归版本
 */
public void postOrderTraverse2(TreeNode root){
    LinkedList<TreeNode> stack1 = new LinkedList<>();
    LinkedList<TreeNode> stack2 = new LinkedList<>();
    TreeNode pNode = root;
    while (pNode != null || !stack1.isEmpty()){
        while (pNode != null){
            stack1.push(pNode);
            stack2.push(pNode);
            pNode = pNode.right;
        }

        if (!stack1.isEmpty()){
            pNode = stack1.pop();
            pNode = pNode.left;
        }
    }
    while (!stack2.isEmpty()){
        TreeNode node = stack2.pop();
        System.out.print(node.val + " ");
    }
}
```

## 层序遍历

思路：先在队列中加入根节点，之后对于任意一个节点来说，在其出队列的时候，访问之，同时如果左孩子和右孩子有不为空的，入队列

```java
/**
 * 层序遍历
 */
public void levelTraverse(TreeNode root){
    if (root == null){
        return;
    }
    LinkedList<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while (!queue.isEmpty()){
        TreeNode node = queue.poll();
        System.out.print(node.val + " ");
        if (node.left != null){
            queue.offer(node.left);
        }
        if (node.right != null){
            queue.offer(node.right);
        }
    }

}
```

## 深度优先遍历 DFS

等同于前序遍历

```java
/**
 * 深度优先遍历  DFS
 */
public void depthOrderTraverse(TreeNode root){
    if (root == null){
        return;
    }
    LinkedList<TreeNode> stack = new LinkedList<>();
    stack.push(root);
    while (!stack.isEmpty()){
        TreeNode node = stack.pop();
        System.out.print(node.val + " ");
        if (node.right != null){
            stack.push(node.right);
        }
        if (node.left != null){
            stack.push(node.left);
        }
    }
}
```

## 广度优先遍历 BFS

等同于层序遍历

```java
/** 
 * 广度优先遍历 BFS 
 */
public void widthOrderTraverse(TreeNode root){    
    if (root == null){        
        return;    
    }    
    LinkedList<TreeNode> queue = new LinkedList<>();    
    queue.offer(root);    
    while (!queue.isEmpty()){        
        TreeNode node = queue.poll();        
        System.out.print(node.val + " ");        
        if (node.left != null){            
            queue.offer(node.left);        
        }        
        if (node.right != null){            
            queue.offer(node.right);        
        }    
    }
}
```



# 参考

1. [二叉树遍历（前序、中序、后序、层次遍历、深度优先、广度优先）My_Jobs的博客-CSDN博客](https://blog.csdn.net/My_Jobs/article/details/43451187)
2. [二叉树后序遍历（递归+非递归）Java_dabusiGin的博客-CSDN博客](https://blog.csdn.net/dabusiGin/article/details/102736180)

