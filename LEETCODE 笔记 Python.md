# LEETCODE 笔记 Python

## 数据结构 data structure

### 1. Linked-list 链表（10道题）

一般head代表的是指向这个链表的头的指针

可以新建一个指针然后对新的指针进行操作

新建node的时候 `new_node = ListNode(int)`



#### Reverse linked-list

- 设定return的新list为prev
- 历遍原始list（head）里的所有值：用while loop 在每次loop 定义 head = head.next()， 当 head.next = none 时，跳出循环
- 在每次loop中：定义list curr = 当前head。
- head = head.next，curr.next = prev,（先把head移走再将curr.next分给prev， 否则head和curr指向同一个东西会改变head的值）
- 把prev移到现在curr的位置，下次loop中current会等于head。



### 2. 树 （包括Binary Search）(31道题)

#### Binary Search

Sort if collection is unsorted

Using a loop or recursion to divide search in half after each compaarsion 

Determine viable candidates in the remaining space

##### Template 1(和邻居无关)

- initial condition:` left = 0, right = length-1`
- termination: `left > right`
- searching left: `right = mid -1`
- searching right : `left = mid +1`

##### Template 2(和右边的邻居相关)

- initial condition: `left = 0, right = length`
- termination: `left = right`
- searching left: `right = mid `
- searching right : `left = mid +1`
- need post- processing(recursive or iterative)

##### Template 3（和左右相邻有关）

- initial condition:`left = 0,right = length-1`
- termination: `left + 1 == right`
- searching left: `right = mid`
- searching right : `left = mid`





### 3. Queue and Stack 栈和队列

#### BTS Templates

两种情况：`do traversal` 和 ` find the shortest path`

In the first round, we process the root node. In the second round, we process the nodes next to the root node; in the third round, we process the nodes which are two steps from the root node; so on and so forth.

第k轮被放到queue里的节点和起始点的最短距离就是k。

##### Template `1`

```java
int BFS(Node root, Node target){

	Queue<Node> queue;  //储存所有将会被经过的节点
	int step = 0;
	add root to queue;   // initialize
	while(queue is not empty){
		step = step+1;
		int size = queue.size();
		for (int i = 0; i < size; ++i){
			Node cur = first node in queue;
			return step if cur is target;
			for (Node next :  the neighbors of cur){
				add next to queue;
				}
			remove the first node from queue;
			}
	}
	return -1;
}


```



##### Template 2(use hashset, never visit a node twice)

```java
int BFS(Node root,Node target){
	Queue<Node> queue;
	Set<Node> visited;
	int setp = 0;
	add root to queue;
	add root to visited;

	while (queue is not empty){
		step = setp+1;
		int size = queue.size();
		for (int i = 0; i < size; ++i){
			Node cur  = the first node in queue;
			return step if cur is target;
			for (Node next : the neighbors of cur){
				if(next is not in visited){
					add next to queue;
					add next to visited;
					}
			remove the first node from queue;
				}
			}		
	}
	return -1;
}
```



#### DFS Template

// returun true if there is a path from cur to target.

boolean DFS(Node cur, Node target, Set<Node> visited){

​	return true if cur is target;

​	for(next :  each neighbor of cur){

​		if  ( next is not in visited){

​			add next to visited

​			return true if DFS(next,target,visited) ==  true;

​		}

​	}

​	return false;

}

### 4. Hashtable 哈希表

### 5.字符串

### 6.数组与矩阵

### 7.图

### 8.位运算







## 算法 Algorithm

### 双指针

### 排序

### 贪心思想

### 二分查找

### 分治

### 搜索

### 动态规划

### 数学



 



indent：

a report:

join reascher group meeting.

make some progress, 

workshop publication 

requirement: after gra 