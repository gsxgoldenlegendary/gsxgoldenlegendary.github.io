---
title: Tree and Binary Tree
date: 2021-12-28 16:04:18
tags: Data Structure
categories: Computer Science
mathjax: true
---

树和二叉树ADT的逻辑结构、存储结构及基本操作：

<!--more-->

# 逻辑结构

## 树

ADT Tree{

数据对象D：D是具有相同特性的数据元素的集合。

数据关系R：若D为空集，则称为空树；
若D仅含一个数据元素，则R为空集，否则R={H}，H是如下二元关系：

1. 在D中存在唯一的称为根的数据元素root，它在关系H下无前驱；
2. 若$D=\{root\}\neq\Phi$，则存在$D-\{root\}$的一个划分$D_1,D_2,\cdots,D_m(m>0)$，对任意$j\neq k(1\leqslant j,k\leqslant m)$，有$D_j\cap D_k=\Phi$，且对任意的$i(1\leqslant i\leqslant m)$，唯一存在数据元素$x_i\in D$，有$<root,x_i>\in H$；
3. 对应于$D=\{root\}$的划分，$H-\{<root,x_1>,\cdots,<root,x_m>\}$有唯一的一个划分$H_1,H_2,\cdots,H_m(m>0)$，对任意$j\neq k(1\leqslant j,k\leqslant m)$有$D_j\cap D_k=\Phi$，且对任意的$i(1\leqslant i\leqslant m)$，$H_i$是$D_i$上的二元关系，$(D_i,\{H_i\})$是一棵符合本定义的树，称为根$root$的子树。

基本操作P：

```c
InitTree(&T);
DestroyTree(&T);
CreateTree(&T,definition);
ClearTree(&T);
TreeEmpty(T);
TreeDepth(T);
Root(T);
Value(T,cur_e);
Assign(T,cur_e,value);
Parent(T,cur_e,value);
LeftChild(T,cur_e);
RightChild(T,cur_e);
InsertChild(&T,&p,i,c);
DeleteChild(&T,&p,i);
TraverseTree(T,Visit());
```

}ADT Tree

## 二叉树

ADT BinaryTree{

数据对象D：D是具有相同特性的数据元素的集合。

数据关系R：若$D=\Phi$，则$R=\Phi$，称BinaryTree为空二叉树；
若$D\neq\Phi$则$R=\{H\}$，H是如下二元关系：

1. 在D中存在唯一的称为根的数据元素root，它在关系H下无前驱；
2. 若$D=\{root\}\neq\Phi$，则存在$D-\{root\}=\{D_l,D_r\}$，且$D_l\cap D_r=\Phi$；
3. 若$D_l\neq\Phi$，则$D_l$中存在唯一的元素$x_l$，$<root,x_l>\in H$，且存在$D_l$上的关系$H_l\subset H$；若$D_r\neq\Phi$，则$D_r$中存在唯一的元素$x_r$，$<root,x_r>\in H$，且存在$D_r$上的关系$H_r\subset H$；$H=\{<root,x_l>,<root,x_r>,H_l,H_r\}$；
4. $(D_l,\{H_l\})$是一棵符合本定义的二叉树，称为根的左子树，$(D_r,\{H_r\})$是一棵符合本定义的二叉树，称为根的右子树。

基本操作P：

```c
InitBiTree(&T);
DestroyBiTree(&T);
CreateBiTree(&T,definition);
ClearBiTree(&T);
BiTreeEmpty(T);
BiTreeDepth(T);
Root(T);
Value(T,e);
Assign(T,&e,value);
Parent(T,cur_r,value);
LeftChild(T,e);
RightChild(T,e);
LeftSibling(T,e);
RightSibling(T,e);
InsertChild(T,p,LR,c);
DeleteChild(T,p,LR);
PreOrderTraverseTree(T,Visit());
InOrderTraverseTree(T,Visit());
PostOrderTraverseTree(T,Visit());
LevelOrderTraverseTree(T,Visit());
```

}ADT BinaryTree

# 存储结构

## 树

### 树的双亲存储表示

```c
#define MAX_TREE_SIZE	//最大节点个数
typedef struct PTNode{
    TElemType data;
    int parent;
}PTNode;
typedef struct{
    PTNode nodes[MAX_TREE_SIZE];
    int r,n;
}PTree;
```



### 树的孩子链表存储表示

```c
typedef struct CTNode{
    int child;
    struct CTNode*next;
}*ChildPtr;
typedef struct{
    TElemType data;
    ChildPtr firstchild;
}CTBox;
typedef struct{
    CTBox nodes[MAX_TREE_SIZE];
    int n,r;
}CTree;
```

### 树的二叉链表（孩子-兄弟）存储表示

```c
typedef struct CSNode{
    ElemType data;
    struct CSNode *firstchild,*nextsibling;
}CSNode,*CSTree;
```

## 二叉树

### 二叉树的顺序存储表示

```c
#define MAX_TREE_SIZE 100
typedef TElemType SqBiTree[MAX_TREE_SIZE];
SqBiTree bt;
```

### 二叉树的二叉线索存储表示

```c
typedef enum Pointer{
    Link,Thread
};
typedef struct BiThrNode{
    TElemType data;
    struct BiThrNode*lchild,*rchild;
    PointerTag LTag,RTag;
}BiThrNode,*BiThrTree;
```

### 赫夫曼树和赫夫曼编码的存储表示

```c
typedef struct{
    unsigned weight;
    unsigned parent,lchild,rchild;
}HTNode,*HuffmanTree;
typedef char** HuffmanCode;
```

# 基本操作

## 二叉树

### 二叉线索存储表示

#### 中序遍历

```c
Status InOrderTraverse(BiTree T,Status(Visit*)(TElemType e)){
    //采用递归
    if(T){
        InOrderTraverse(T->lchild);
        Visit(T->data);
        InOrderTraverse(T->rchild);
    }else
        return OK;
}//InOrderTraverse
```

```c
Status InOrderTraverse(BiTree T,Status(Visit*)(TElemType e)){
    //采用非递归
    InitStack(S);
    Push(S,T);
    while(!StackEmpty(S)){
       while(GetTop(S,e)&&e)
           Push(S,e->lchild);
        Pop(S,e);
        if(!StackEmpty(S)){
            Pop(S,e);
            Visit(e->data);
            Push(S,p->rchild);
        }//if
    }//while
}//InOrderTraverse
```

#### 先序遍历

```c
Status PreOrderTraverse(BiTree T,Status(Visit*)(TElemType e)){
    if(T){
        Visit(T->data);
        PreOrderTraverse(T->lchild);
        PreOrderTraverse(T->rchild);
    }else
        return OK;
}//PreOrderTraverse
```

#### 后序遍历

```c
Status PostOrderTraverse(BiTree T,Status(Visit*)(TElemType e)){
    if(T){
        PostOrderTraverse(T->lchild);
        PostOrderTraverse(T->rchild);
        Visit(T->data);
    }else
        return OK;
}//PostOrderTraverse
```

#### 构建

```c
Status CreateBiTree(BiTree &T){
    scanf(&ch);
    if(ch==RefValue)
        T=NULL;
    else{
        T=(BiTNode*)malloc(sizeof(BiTNode));
        if(!T)
            exit(OVERFLOW);
        CreateBiTree(T->lchild);
        CreateBiTree(T->rchild);
    }//else
    return OK;
}//CreateBiTree
```

#### 计算结点个数

```c
int Count(BiTree T){
    if(!T)
        return 0;
    return Count(T->lchild)+Count(T->rchild)+1;
}//Count
```

