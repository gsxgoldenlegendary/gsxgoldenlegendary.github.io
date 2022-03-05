---
title: Graph
date: 2021-12-28 16:04:35
tags: Data Structure
categories: Computer Science
mathjax: true
---

图ADT的逻辑结构、存储结构及基本操作：

<!--more-->

# 逻辑结构

## 图

ADT Graph{

数据对象V：$V$是具有相同特性的数据元素的集合，称为顶点集。

数据关系R：
$$
R=\{VR\}
$$

$$
VR=\{<v,w>|v,w\in V且P(v,w),<v,w>表示从v到w的弧，谓词P(v,w)定义了弧<v,w>的意义或信息\}
$$

基本操作P：

```c
CreatGraph(&G,V,VR);
DestroyGraph(&G);
LocateVex(G,u);
GetVex(G,v);
PutVex(&G,v,value);
FirstAdjVex(G,v,&w);
NextAdjVex(G,v,&w);
InsertVex(&G,v);
DeleteVex(&G,v);
InsertArc(&G,v,w);
DeleteArc(&G,v,w);
DFSTraverse(G,Visit());
BFSTraverse(G,Visit());
```

}ADT Graph

# 存储结构

## 图的数组（邻接矩阵）存储表示

```c
#define INFINITY INT_MAX
#define MAX_VERTEX_NUM 20
typedef struct ArcCell{
    VRType adj;
    InfoType *info;
}ArcCell,AdjMatrix[MAX_VERTEX_NUM][MAX_VERtEX_NUM];
typedef struct{
    VertexType vexs[MAX_VERTEX_NUM];
    AdjMatrix arcs;
    int vexnum,arcnum;
    GraphKind kind;
}MGraph;
```

## 图的邻接表存储表示

```c
#define MAX_VERTEX_NUM 20
typedef struct ArcNode{
    int adjvex;
    struct ArcNode* next;
    InfoType* info;
}ArcNode;
typedef struct VNode{
    VertexType data;
    ArcNode* firstarc;
}VNode,AdjList[MAX_VERTEX_NUM];
typedef struct{
    AdjList vertices;
    int vexnum,arcnum;
    int kind;
}ALGraph;
```

## 有向图的十字链表存储表示

```c
#define MAX_VERTEX_NUM 20
typedef struct ArBox{
    int tailvex,headvex;
    struct ArcBox *hlink,*tlink;
    TnfoType* info;
}ArcBox;
typedef struct VexNode{
    VertexType data;
    ArcBox *firstin,*firstout;
}VexNode;
typedef struct{
    VexNode xlist[MAX_VERTEX_NUM];
    int vexnum,arcnum;
}OLGraph;
```

# 基本操作

## 图的数组（邻接矩阵）存储表示

### 顶点定位

```c
int LocateVex(MGraph &G,VexType &vp){
    for(k=0;k<G.vexnum;++k)
        if(G.vexs[k]==vp)
            return k;
    return -1;
}
```

### 构造

```c
Status CreateUDN(MGraph &G){
    scanf(&G.vexnum,&G.arcnum,&IncInfo);
    for(i=0;i<G.vexnum;++i)
        scanf(&G.vex[i]);
    for(i=0;i<G.vexnum;++i)
        for(j=0;i<G.vexnum;++j)
            G.arcs[i][j]={INFINITY,NULL};
    for(i=0;i<G.arcnum;++i){
        scanf(&u,&v,&w);
        i=LocateVex(G,v1);
        j=LocateVex(G,v2);
        G.arcs[i][j].w=w;
        if(IncInfo)
            Input(*G.adj[i][j].Info);
        G.arcs[j][i]=G.arcs[i][j];
    }//for
    return OK;
}//CreateUDN
```

### 增加顶点

```c
int AddVertex(MGraph &G,VexType vp){
    int k,j;
    if(G.vexnum>=MAX_VERTEX_NUM||LocateVex(G,vp)==EOF)
        return EOF;
    k=G.vexnum;
    G.vertices[G.vexnum++]=vp;
    if(G.kind==DG||G.kind==UDG)
        for(j=0;j<G.vexnum;++j)
            G.arcs[j][k].w=G.arcs[k][j].w=0;
    else
         for(j=0;j<G.vexnum;++j)
            G.arcs[j][k].w=G.arcs[k][j].w=INFINITY;
    return k;
}//AddVertex
```

### 增加弧

```c
Status AddArc(MGraph &G,ArcType arc){
    if(k=LocateVex(G,arc.vex1)==EOF||j=LocateVex(G.arc.vex2)==EOF)
        return ERROR;
    if(G.kind==DG||G.kind==DN){
        G.arcs[k][j].w=arc.w;
        G.arcs[k][j].info=arc.info;
    }else{
        G.arcs[k][j].w=arc.w;
        G.arcs[k][j].info=arc.info;
        G.arcs[j][k].w=arc.w;
        G.arcs[j][k].info=arc.info;
    }//else
    return OK;
}//AddArc
```

## 图的邻接表存储表示

### 构建

```c
Status Create_Graph(ALGraph &G){
    scanf(&G.kind);
    G.vexnum=0;
    return OK;
}//Create_Graph
```

### 顶点定位

```c
int LocateVex(ALGraph G,VexType vp){
    for(k=0;k<G.vexnum;++k)
        if(G.vertices[k].data==vp)
            return k;
    return EOF;
}//LocateVex
```

### 增加顶点

```c
int AddVertex(ALGraph &G,VertexType vp){
    if(G.vexnum>=MAX_VERTEX_NUM||LocateVex(G,vp)!=EOF)
        return EOF;
    G.veritces[G.vexnum].data=vp;
    G.vertices[G.vexnum].firstarc=NULL;
    return ++G.vexnum;
}//AddVertex
```

### 增加弧

```c
int AddArc(ALGraph &G,ArcType arc){
    if(k=LocateVex(G,arc.vex1)==EOF||j=LocateVex(G,arc.vex2)==EOF)
        return EOF;
    p=(ArcNode*)malloc(sizeof(ArcNode));
    if(!p)
        exit(OVERFLOW);
    p->adjvex=arc.vex1;
    p->info=arc.info;
    p->next=NULL;
    q=(ArcNode*)malloc(sizeof(ArcNode));
    if(!q)
        exit(OVERFLOW);
    q->adjvex=arc.vex2;
    q->info=arc.info;
    q->next=NULL;
    if(G.kind==UDG||G.kind==UDN){
        q->nextarc=G.vertices[k].firstarc;
        G.vertices[k].firstarc=q;
        p->nextarc=G.vertices[j].firstarc;
        G.vertices[k].firstarc=p;
    }else{
        q->nextarc=G.vertices[k].firstarc;
        G.vertices[k].firstarc=q;
    }//else
    return OK;
}//AddArc
```

### 深度优先搜索遍历

```c
bool visited[MAX];
Status(*VisitFunc)(int v);
void DFSTranverse(Graph G,Status(*Visit)(int v)){
    //时间复杂度O(n+e)
    VisitFunc=Visit;
    for(v=0;v<G.vexnum;++v)
        visit[v]=false;
    for(v=0;v<G.vexnum;++v)
        if(!visited[v])
            DFS(G,v);
}//DFSTraverse
void DFS(Graph G,int v){
    visited[v]=true;
    VisitFunc(v);
    for(w=FirstAdjVex(G,v);w!=EOF;NextAdjVex(G,v,w))
        if(!visited[w])
            DFS(G,w);
}//DFS
```



### 广度优先搜索遍历

```c
void BFSTraverse(Graph G,Status(*Visit)(int v)){
    for(v=0;v<G.vexnum;++v)
        visited[v]=false;
    InitQueue(Q);
    for(v=0;v<G.vexnum;++v)
        if(!visited[v]){
            visited[v]=true;
            Visit(v);
            EnQueue(Q,v);
            while(!QueueEmpty(Q)){
                DeQueue(Q,e);
                for(w=FirstAdjVex(G,e);w!=EOF;NextAdjVex(G,e,w))
                if(!visited[w]){
                    visited[w]=true;
                    Visit(w);
                    EnQueue(Q,w);
                }//if
            }//while
        }//if
}//BFSTraverse
```

