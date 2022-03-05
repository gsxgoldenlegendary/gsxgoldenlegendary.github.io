---
title: Searching List
date: 2021-12-28 16:05:28
tags: Data Structure
categories: Computer Science
---

查找表ADT的逻辑结构、存储结构及基本操作：

<!--more-->

# 逻辑结构

## 静态查找表

ADT StaticSearchTable{

数据对象D：D是具有相同特性的数据元素的集合，各个数据元素均含有类型相同，可唯一标识数据元素的关键字。

数据关系R：数据元素同属一个集合。

基本操作P：

```c
Create(&ST,n);
Destroy(&ST);
Search(ST,key);
Traverse(ST,Visit());
```

}ADT StaticSearchTable

## 动态查找表

ADT DynamicSearchTable{

数据对象D：D是具有相同特性的数据元素的集合，各个数据元素均含有类型相同，可唯一标识数据元素的关键字。

数据关系R：数据元素同属一个集合。

基本操作P：

```c
InitDSTable(&DT);
DestroyDSTable(&DT);
SearchDSTable(DT,key);
InsertDSTable(&DT,e);
DeleteDSTable(&DT,key);
TraverseDSTable(DT,Visit());
```

}ADT StaticSearchTable

# 存储结构

## 静态查找表的顺序存储结构

```c
typedef struct{
    ElemType* elem;
    int length;
}SSTable;
```

## 二叉排序树的存储结构

```c
typedef struct BSTNode{
    ElemType data;
    int bf;
    struct BSTNode *lchild,*rchild;
}BSTNode,*BSTree;
```

## B-树的存储结构

```c
#define m 3;
typedef struct BTNode{
    int keynum;
    struct BTNode *parent;
    KeyType key[m+1];
    struct BTNode *ptr[m+1];
    Record *recptr[m+1];
}BTNode,*BTree;
typedef struct{
    BTNode *pt;
    int i;
    int tag;
}Result;
```

## 键树的孩子兄弟链表存储结构

```c
#define MAXKEYLEN 16
typedef struct {
    char ch[MAXKEYLEN];
    int num;
}KeysType;
typedef enum {
    LEAF,
    BRANCH
}NodeKind;
typedef struct DLTNode{
    char symbol;
    struct DLTNode *next;
    NodeKind kind;
    union{
        Record* infoptr;
        struct DLTNode *first;
    }
}DLTNode,*DLTree;
```

## 键树的多重链表存储结构

```c
typedef struct TrieNode{
    NodeKind kind;
    union {
        struct{
            KeysType K;
            Record* infoptr;
        }lf;
        struct{
            TrieNode *ptr[27];
            int num;
        }bh;
    };
}TrieNode,*TrieTree;
```

## 开放地址哈希表的存储结构

```c
int hashsize[]={997,...};
typedef struct{
    ElemType *elem;
    int count;
    int sizeindex;
}HashTable;
```

# 基本操作

## 顺序查找表

### 查找

```c
int Search_Seq(SSTable ST,KeyType key){
    ST.elem[0].key=key;
    for(i=ST.length;ST.elem[i].key!=key;--i){}
    return i;
}//Search_Seq
```



### 有序表的折半查找

```c
int Search_Bin(SSTable ST,KeyType key){
    low=1;
    high=ST.length;
    while(low<=high){
        mid=(low+high)/2;
        if(key==ST.elem[mid].key)
            return mid;
        else if(key<ST.elem[mid].key)
            high=mid-1;
        else 
            low=mid+1;
    }//while
}//Search_Bin
```

### 分块查找

```c
typedef struct IndexType{
    keyType maxkey;
    int startpos;
}Index;
int Block_search(RecType ST[],Index ind[],KeyType key,int n,int b){
    //在分块索引表中查找关键字为key的记录，表长为n，块数为k
    for(i=0;i<b&&LT(ind[i].maxkey,key);++i){}
    if(i>b)
        return 0;
    for(j=ind[i].startpos;;j<n&&LQ(ST[j].key,ind[i].maxkey))
        if(EQ(ST[j].key,key))
            break;
    if(j>=n||!EQ(ST[j].key,key))
        j=0;
    return j;
}//Block_search
```

## 二叉排序树

### 查找

```c
Status SearchBST(BiTree T,KeyType key,BitNode* f,BitNode* p){
    if(!T){
        p=f;
        return FALSE;
    }//if
    if(EQ(key,T->data.key)){
        p=T;
        return TRUE;
    }//if
    if(LT(key,T->data.key)){
        f=T;
        return SearchBST(T->lchild,key,f,p);
    }else{
        f=T;
        return SearchBST(T->rchild,key,f,p);
    }//else
}//SearchBST
```

### 插入新数据

```c
Status InsertBST(BiTree &T,ElemType e){
    if(!SearchBST(T,e.key,NULL,p)){
        s=(BiTree)malloc(sizeof(BiTNode));
        s->data=e;
        s->lchild=s->rchild=NULL;
        if(!p)
            T=s;
        else if(LT(e.key,p->data.key))
            p->lchild=s;
        else 
            p->rchild=s;
        return TRUE;
    }else
        return FALSE;
}//InsertBST
```

## 平衡二叉树

### 平衡化旋转（LL）

```c
void LL_rotate(BSTNode *a){
    b=a->lchild;
    a->lchild=b->rchild;
    b->rchild=a;
    a->bf=b->bf=0;
    a=b;
}//LL_rotate
```

### 平衡化旋转（LR）

```c
void LR_rotate(BSTNode *a){
    b=a->lchild;
    c=b->rchild;
    b->rchild=c->lchild;
    a->lchild=c->rchild;
    c->lchild=b;
    c->rchild=a;
    if(c->bf==1){
        a->bf=-1;
        b->bf=0;
        c->bf=0;
    }else if(c->bf==0){
        a->bf=0;
        b->bf=0;
    }else{
        a->bf=0;
        b->bf=1;
        c->bf=0;
    }//else 
    a=c;
}//LR_rotate
```

