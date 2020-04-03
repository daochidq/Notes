LEETCODE 刷题日记

目标：50天 200道题----------一天4道

争取在5.17搞定！！！！！

刷题按照GitHub上的总结[目录](https://github.com/CyC2018/CS-Notes/blob/master/notes/Leetcode%20%E9%A2%98%E8%A7%A3%20-%20%E7%9B%AE%E5%BD%95.md)来，先数据结构再算法

每道题争取做详细笔记 5分钟内没有想法就看答案

# 努力啊！！！

### 打卡

- [x] DAY 1
- [x] DAY 2
- [x] DAY 3
- [x] DAY 4
- [x] DAY 5
- [x] DAY 6
- [x] DAY 7
- [ ] DAY 8
- [ ] DAY 9
- [ ] DAY 10
- [ ] DAY 11
- [ ] DAY 12
- [ ] DAY 13
- [ ] DAY 14
- [ ] DAY 15

## DAY 1 3.28

### 160. Intersection of Two Linked Lists(easy)找两个链表的交点 ✅ 

```html

A:          a1 → a2
                    ↘
                      c1 → c2 → c3
                    ↗
B:    b1 → b2 → b3

```

方法：two points 运用两个指针

pointer1 = headA

pointer2 = headB

让两个指针分别历遍A和B 到尽头之后 对调

假设A 的单独部分长a B 单独的部分长b 一起的部分长c：a+c+b= b+c+a

如果没有共同的部分 a+b=b+a

```python
def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
  pa = headA
  pa = headB
  while pa != pb:
    pa = headB if pa.next is None else pa.next
    pb = headA if pb.next is None else pb.next
    
 	return pa
    
```





### 206. Reverse Linked List (Easy)反转链表✅

- 设定return的新list为prev
- 历遍原始list（head）里的所有值：用while loop 在每次loop 定义 head = head.next()， 当 head.next = none 时，跳出循环
- 在每次loop中：定义list curr = 当前head。
- head = head.next，curr.next = prev,（先把head移走再将curr.next分给prev， 否则head和curr指向同一个东西会改变head的值）
- 把prev移到现在curr的位置，下次loop中current会等于head。



```python
def reverseList(self, head: ListNode) -> ListNode:
  prev = None
  while head.next is not None:
    curr = head
    head = head.next
    curr.next = prev
    prev = curr
  return prev
```



### 21. Merge Two Sorted Lists (Easy) 合并两个有序的链表✅

用递归的方法 

当L1 或者L2 是None的时候 return 另外一个

如果L1 的第一个值比L2 的第一个值大：就让L2 = L1和L2.next 合并出来的结果

反之就让 L1 = L1.next 和L2 合并出来的结果

以此递归 最后得到的就是合并完成的链表

```python
def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
  if l1 is None:
    return l2
  elif l2 is None:
    return l1
  elif l1.val > l2.val:
    l2 = self.mergeTwoLists(l1,l2.next)
    return l2
  else:
    l1 = self.mergeTwoLists(l1.next,l2)
    return l1
```

此题还可以用迭代的方法做，待增加

### 83. Remove Duplicates from Sorted List (Easy)从有序链表中删除重复节点✅

```html
Given 1->1->2, return 1->2.
Given 1->1->2->3->3, return 1->2->3.
```

新建一个指针cur = head

while loop历遍整个head 当cur或者cur.next 是空的时候 跳出循环

比较当前cur.val 和cur.next.val

如果一样的话说明重复了 就直接让cur的下一个等于cur.next.next 跳过原本的下一个 这个时候cur指的位置并没有发生改变

如果不一样的话 将cur的指针指到cur.next

⚠️最后返回的是原链表head （return head 等于返回的是这个链表的头指针 代表了整个链表）

```python
def deleteDuplicates(self, head: ListNode) -> ListNode:
  cur = head
  while cur != None and cur.next != None:
    if cur.val == cur.next.val:
      cur.next = cur.next.next
    else:
      cur = cur.next
  return head
```



## DAY 2 3.29

### 19. Remove Nth Node From End of List (Medium) 删除链表中的倒数第N个节点✅

```html
Given linked list: 1->2->3->4->5, and n = 2.
After removing the second node from the end, the linked list becomes 1->2->3->5.
```

方法：two pointers 运用一快一慢两个指针

用一个for loop让两个指针之间相差n个节点，这样当快的指针指到最后一个节点的时候 慢的指针正好指到倒数第n+1个节点

然后用一个while loop历遍快的指针之后的节点 当指到最后一个节点时跳出循环

慢的指针的下一个 = 下一个的下一个 

⚠️ 当需要删除的是第一个节点时，这时候for loop完之后 快的指针已经指向最后一个节点的下一个（none）此时直接return head.next

```Python
def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
  pa = head
  pb = head
  for i in range(n):
    pa = pa.next
  if not pa:
    return head.next
  while pa.next:
    pa = pa.next
    pb = pb.next
    
  pb.next = pb.next.next
  return head
```



### 24. Swap Nodes in Pairs (Medium) 交换链表中相邻的节点✅

```html
Given 1->2->3->4, you should return the list as 2->1->4->3.
要求不能改变val的值
```

这个问题需要新建一个dummy node 放在原先list的前面 `dummy ->1->2->3->4`

再新建一个指针cur 指向dummy node

所以我们每次需要操作的就是 cur cur.next和cur.next.next这三个节点

用一个while loop 当cur.next和cur.next.next 都有值的时候：

新建两个指针pa,pb分别指向cur.next和cur.next.next

然后令cur的下一个等于pb，令pa.next = pb.next，令pb.next = pa，注意顺序

最后让cur往后移两位

注意⚠️ return的是dummy.next 因为dummy一直指向的是链表的最最开始

```Python
def swapPairs(self, head: ListNode) -> ListNode:
  dummy = ListNode(-1)
  dummy.next = head
  cur = dummy
  while cur.next and cur.next.next:
    pa = cur.next
    pb = cur.next.next
    cur.next = pb
    pa.next = pb.next
    pb.next = pa
    
    cur = cur.next.next
  return dummy.next
```



### 445. Add Two Numbers II (Medium) 链表求和✅

```html
Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7
```

将两个链表的值分别存成两个int， 然后相加 

最后再将得到的数变成新的链表

```Python
def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
  if not l1:
    return l2
  elif not l2:
    return l1
  else:
    l1_num = l2_num = 0
    while l1:
      l1_num = l1_num*10 + l1.val
      l1 = l1.next
    while l2:
      l2_num = l2_num*10 + l2.val
      l2 = l2.next
    s = l1_num + l2_num
    str_s = str(s)
    new_list = ListNode(int(str_s[0])
    new_head = new_list
    for i in range(1,str_s):
      new_head.next = ListNode(int(str_s[i]))
      new_head = new_head.next
    return new_list
```



### 234. Palindrome Linked List (Easy)回文链表✅

将链表里的值存到一个list里 然后反转list 看是否相等

```Python
def isPalindrome(self, head: ListNode) -> bool:
  val = []
  cur = head
  while cur:
    val.append(cur.val)
    cur = cur.next
  return val == val[::-1]
```



## DAY 3 3.30

### 725. Split Linked List in Parts(Medium)分隔链表✅

```html
Input:
root = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], k = 3
Output: [[1, 2, 3, 4], [5, 6, 7], [8, 9, 10]]
Explanation:
The input has been split into consecutive parts with size difference at most 1, and earlier parts are a larger size than the later parts.
```

用一个for loop 或者while loop 先算出链表的长度N

用N除以k得到除数和余数 除数代表每个part里有几个node 余数代表开头有几个part是多一个node的

新建一个空的list 长度为k 

新建指针prev指向none

新建cur指针指向head

用for loop循环到k：

list的第i个值设为cur

再套一个for loop循环 代表每个part

将prev指向cur，cur = cur.next

如果prev有值 则将prev的下一个指向空（断开链表）

```python
def splitListToParts(self, root: ListNode, k: int) -> List[ListNode]:
  cur = root
  for N in range(1001):
    cur = cur.next
    if not cur:
      break
  m = N // k
  n = N % k
  res = [None for _ in range(k)]
  prev = None
  cur = root
  for i in range(k):
    res[i] = cur
    for j in range(m +(1 if n >i else 0)):
      prev = cur
      cur = cur.next
    if prev:
      prev.next = None
  return res
    
```



### 328. Odd Even Linked List (Medium) 链表元素按奇偶数聚集✅

```html
Input: 1->2->3->4->5->NULL
Output: 1->3->5->2->4->NULL
Input: 2->1->3->5->6->4->7->NULL
Output: 2->3->6->7->1->5->4->NULL
```

⚠️是把节点按照节点的奇偶顺序重排 而不是值

新建odd指针指向head，even指针指向head.next

新建evenhead指针指向even的头

用while循环 当even或者even的下一个没有值的时候跳出循环

在循环中：odd.next指向even.next

移动odd到下一个值

even.next指向odd.next

移动even指针到下一个值

出循环后将odd的下一个指向evenhead

```python
def oddEvenList(self, head: ListNode) -> ListNode:
  odd = head
  even = head.next
  evenhead = even
  while even and even.next:
    odd.next = even.next
    odd = odd.next
    even.next = odd.next
    even = even.next
  odd.next = evenhead
  return head
```



### 104. Maximum Depth of Binary Tree (Easy) 树的高度✅

用递归的方法

每个节点都返回1+下个节点的高度

```Python
def maxDepth(self, root: TreeNode) -> int:
  if not root:
    return 0
  else:
    l = self.maxDepth(root.left)
    r = self.maxDepth(root.right)
    return 1 + max(l,r)
```



### 110. Balanced Binary Tree (Easy)平衡树✅

```html
    3
   / \
  9  20
    /  \
   15   7
平衡树左右子树高度差都小于等于 1
```

结合树的高度那一题 新建一个helper function来算子树的高度以及是否平衡

如果左边的高度和右边的高度相差大于1 则返回-1

如果左边或者右边的高度等于-1，说明某一边不平衡则整个树不平衡也返回-1

```Python
def maxdepth(root):
  if not root:
    return 0
  else:
    l = self.maxDepth(root.left)
    r = self.maxDepth(root.right)
  if abs(l-r) >1 or l == -1 or r == -1:
    return -1
  else:
    return 1+max(l,r)
    
def isBalanced(self, root: TreeNode) -> bool:
  x = maxdepth(root)
  return x != -1
```



## DAY 4 3.31

### 543. Diameter of Binary Tree (Easy)两节点的最长路径✅

```html
Input:

         1
        / \
       2  3
      / \
     4   5

Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].
```

运用递归的方法

新建一个self.max_l用来储存最长的路径的长度

新建一个function depth

和之前算深度的方程差不多 但是每次更新self.max_l的值，如果每次递归得到的左边的树的深度和右边的树的和比self.max_l大 则更新self.max_l的值

最后返回self.max_l

```python
def diameterOfBinaryTree(self, root: TreeNode) -> int:
  if not root:
    return 0
  self.max_l = 0
  def depth(node):
    if not node:
      return 0
    l = depth(node.left)
    r = depth(node.right)
    self.max_l = max(self.max_l,l+r)
    return 1+max(l,r)
  depth(root)
  return self.max_l
```



###226. Invert Binary Tree (Easy) 反转树✅

```html
     4                     4
   /   \                 /   \
  2     7      ----->   7     2
 / \   / \            /  \    / \
1   3 6   9          9    6  3   1
```

从树的最低端开始翻转，用递归的方法

```python
def invertTree(self, root: TreeNode) -> TreeNode:
  if not root:
    return None
  l = self.invertTree(root.left)
  r = self.invertTree(root.right)
  root.left = r
  root.right = l
  return root
```



### 617. Merge Two Binary Trees (Easy)合并两棵树✅

```html
Input:
       Tree 1                     Tree 2
          1                         2
         / \                       / \
        3   2                     1   3
       /                           \   \
      5                             4   7

Output:
         3
        / \
       4   5
      / \   \
     5   4   7
```

当节点重合的时候 值相加，当不重合的时候用有值的那个

和链表的合并有一点像，用递归的方法

从root开始合并

```python
def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
  if not t1:
    return t2
  elif not t2:
    return t1
  else:
    t1.val += t2.val
    t1.left = self.mergeTrees(t1.left,t2.left)
    t1.right = self.merTrees(t1.right,t2.right)
  return root
```



### 112. Path Sum (Easy) 判断路径和是否等于一个数✅

```html
Given the below binary tree and sum = 22,

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1

return true, as there exist a root-to-leaf path 5->4->11->2 which sum is 22.
```

这道题也是用递归的方法

从头开始找路的话 当找到最后一个节点应该满足的条件有：1 此节点是叶子节点，2 此节点的值应该等于sum减掉之前节点的的值

在递归中 每次都用sum 减掉当前节点的值，并判断此时sum的值是否为零 并且判断此节点是不是叶子节点 如果是的话就是返回true

因为有可能这条路在左边也有可能在右边 所以我们返回的是or

```python
def hasPathSum(self, root: TreeNode, sum: int) -> bool:
  if not root:
    return False
  sum -= root.val
  if not root.left and not root.right and sum == 0:
    return True
  return self.hasPathSum(root.left,sum) or self.hasPathSum(root.right,sum)
```



## DAY 5 4.1

### 437. Path Sum III (Easy)统计路径和等于一个数的路径数量✅

```html
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```

这道题运用双重递归的方法 ⚠️也可以用hashtable（还没尝试）

一重递归历遍所有节点，二重递归是把每个节点当成root看有没有path，时间复杂度可达到 $N^2$

先新建一个helper function 叫做pathnum，来记录当前输入节点下有多少条路径

在pathnum中建一个counter= 0 当当前节点的值等于sum的时候，counter加1

然后递归到当前节点的左节点(这时候的sum应该减掉当前节点的值) 得到的值加上counter

在递归右节点，同样的加上counter，返回counter的值

原方程返回的是 在root节点用pathnum找到的路 + 递归左节点 + 递归右节点

⚠️今天的题目中大部分都用到这样的技巧，就是最后返回的是helper(root) + 原方程（左节点）+ 原方程（右节点）

```python
def pathSum(self, root: TreeNode, sum: int) -> int:
  if not root:
    return 0 
  def pathnum(node,sum):
    counter = 0
    if node.val == sum:
      counter += 1
    counter += pathnum(node.left,sum-node.val)
    counter += pathnum(node.right, sum-node.val)
    return counter  
  return pathnum(root) + self.pathSum(root.left,sum) + self.pathSum(root.right,sum)
    
```



### 572. Subtree of Another Tree (Easy)子树✅

```html
Given tree s:
     3
    / \
   4   5
  / \
 1   2

Given tree t:
   4
  / \
 1   2

Return true, because t has the same structure and node values with a subtree of s.

Given tree s:

     3
    / \
   4   5
  / \
 1   2
    /
   0

Given tree t:
   4
  / \
 1   2

Return false.
```

这道题还是运用递归的方法，来判断每个节点是否相同

如果s为空，则返回False

新建helper function (isidentical): 如果两个节点的值相同 并且他们的左节点相同 他们的右节点也相同 则认为这两个节点相同

edge case：当两个节点都为空时，认为两个节点相同。所以当节点为叶子节点时，值相同即为相同

最后原方程的返回值为：helper(初始的两个节点 t1,t2) and 原方程（t1左节点,t2）and  原方程（t1.右节点,t2）

```python
def isSubtree(self, s: TreeNode, t: TreeNode) -> bool:
  if not s:
    return False
  def isidentical(n1,n2):
    if not n1 and not n2:
      return True
    elif not n1 or not n2:
      return False
    elif n1.val == n2.val and isidentical(n1.left,n2.left) and isidentical(n1.right,n2.right):
      return True
    return False
  return isidentical(s,t) and self.isSubtree(s.left,t) and self.isSubtree(s.right,t)
```



### 101. Symmetric Tree (Easy)树的对称✅

```html
For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

    1
   / \
  2   2
 / \ / \
3  4 4  3
 

But the following [1,2,2,null,3,null,3] is not:

    1
   / \
  2   2
   \   \
   3    3
```

这道题同样的运用递归的方法来判断两个节点是否是镜像的

如果树的根为空的话 返回True

新建一个helper function (ismirror): 此方程有两个输入。当两个节点的值是一样的 并且第一个节点的左节点等于第二个节点的右节点 第一个节点的右节点等于第二个节点的左节点的时候 判定这两个节点为镜像节点。

edge case：如果节点为空的话 返回True 所以当节点为叶子节点的时候只要值相等便是镜像

最后原方程的返回值为： ismirror(root,root)

```python
def isSymmetric(self, root: TreeNode) -> bool:
  if not root:
    return True
  def ismirror(n1,n2):
    if not n1 and not n2:
      return True
    elif not n1 or not n2:
      return False
    else:
      return n1.val == n2.val and ismirror(n1.left,n2.right) and ismirror(n1.right,n2.left)
  return ismirror(root,root)
```



### 111. Minimum Depth of Binary Tree (Easy)最短路径✅

这道题和最长路径类似 不过是一个最长最短

还是递归 需要注意的是当只有一条树枝的时候最短路径就是那条树枝的长度（有点坑）

```Python
def minDepth(self, root: TreeNode) -> int:
  if not root:
    return 0
  l = self.minDepth(root.left)
  r = self.minDepth(root.right)
  if l == 0 or r == 0:
    return 1 + max(l,r)
  return 1 + min(l,r)
```



## DAY 6 4.2

### 404. Sum of Left Leaves (Easy)统计左叶子节点的和✅

```html
 		3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```

使用递归的方法

这道题需要注意的是必须是左边的叶子节点才行

所以需要一个helper function来决定这个节点是不是叶子节点

决定叶子节点的要素：没有左右子节点，节点有值

在主方程中：如果一个节点的左节点是叶子节点的话 则返回这个节点左节点的值 + 原方程（这个节点的右节点）

返回 原方程（左节点）+ 原方程（右节点）

```python
def sumOfLeftLeaves(self, root: TreeNode) -> int:
  if not root:
    return 0
  def isleave(node):
    if not node:
      return False
    elif not node.left and not node.right:
      return True
    return False
  if isleave(root.left):
    return root.left.val + self.sumOfLeftLeaves(root.right)
  return self.sumOfLeftLeaves(root.left) + self.sumOfLeftLeaves(root.right)
```



### 687. Longest Univalue Path (Easy) 相同节点值的最大路径长度✅

```html
             1
            / \
           4   5
          / \   \
         4   4   5

Output : 2
```

用递归的方法，这道题也不简单

先新建一个全局变量ans来记录最长的路径 初始值为0

新建helper function来判断每个节点之后有几条路径

在helper function中：初始化两个路径的值都为0(pr,pl)，当节点为空时返回0 让l为左子节点递归后返回的值，让r为右子节点递归后返回的值。因为每个节点都得到下个左右子节点得到的值，当左子节点有值并且和当前节点的值相等时 pl = l+1，同理得到pr=r+1。当左右子节点都为叶子节点时，l和r的值其实都是0. 然后更新ans，取（原先的ans和pr+pl中较大的一个）。注意，因为我们可以有4-4-4这样的路径，所以选路径的时候pr，pl可以相加。返回 max(pr,pl)

最后在原方程中从root跑一遍helper function

返回ans

```python
def longestUnivaluePath(self, root: TreeNode) -> int:
  self.ans = 0
  def path(node):
    pr = pl = 0
    if not node:
      return 0
    l = path(node.left)
    r = path(node.right)
    if node.left and node.left.val == node.val:
      pl = l + 1
    if node.right and node.right.val == node.val:
      pr = r + 1
    self.ans = max(self.ans,pr+pl)
    return max(pr,pl)
  path(root)
  return self.ans
```



### 337. House Robber III (Medium) 间隔历遍✅

```html
   	 3
    / \
   2   3
    \   \
     3   1
Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
```

好难啊这道题

第一次用递归的方法做了，结果时间复杂度过于大

改用DP的方法（吧，也可能不是），用了一个list吧（也可以不用list应该）

这道题主要是求这个小偷在不偷相邻的两个房子的情况下最多能偷到多少钱

可以简化为在每一个节点都判断要不要偷这个节点，每个节点生成两个值[偷，不偷]来代表在两种情况下把现在这个节点当成根节点所能偷到的数目。

当节点为空的时候 两个值都是0【0，0】

新建helper function，在方程中递归的判断要不要偷这个节点 

左子节点得到两个值，右子节点也得到两个值

当前节点偷的值则为，当前节点的值+左不偷+右不偷

当前节点不偷的值则为，左边值较大的选项+右边值较大的选项

原方程返回历遍整棵树之后 数值较大的那个选项

```python
def rob(self, root: TreeNode) -> int:
  def decision(node):
    if not node:
      return [0,0]
    left = decision(node.left)
    right = desicon(node.right)
    robb = node.val + left[0] + right[0]
    notrob = max(left[0],left[1]) + max(right[0],right[1])
    return [robb,notrob]
  return max(decision(node))
```



###671. Second Minimum Node In a Binary Tree (Easy) 找出二叉树中第二小的节点✅

```html
Input:
   2
  / \
 2   5
    / \
    5  7

Output: 5
```

因为题目设置，根节点的值总是小于它的子节点的值

可以用dfs的方法来做

将根节点的值储存为最小值

当节点为空时，返回-1

新建方程dfs，在方程中：

节点为空时，返回-1

当当前节点的值大于最小值时：返回当前节点的值

令l= 左子节点递归得到的值，r=右子节点递归的值

当l，r都不为-1时 返回较小的那个，否则返回不是-1的那个

原方程返回dfs(root)

```python
def findSecondMinimumValue(self, root: TreeNode) -> int:
  if not root:
    return -1
  min_num = root.val
  def dfs(node):
    if not root:
      return -1
    if node.val > min_num:
      return node.val
    l = dfs(node.left)
    r = dfs(node.right)
    if l == -1:
      return r
    if r == -1:
      return l
    return min(l,r)
  return dfs(root)
    
```



## DAY 7 4.3

### 637. Average of Levels in Binary Tree (Easy) 一棵树每层节点的平均数✅

```html
Input:
    3
   / \
  9  20
    /  \
   15   7
Output: [3, 14.5, 11]
```

这道题主要是一个层次遍历，运用BFS的方法来解决

BFS 主要是需要用到一个queue来储存每一层的节点，然后用while loop在当queue不为空的情况下循环，套路都是类似的。

当queue 不为空时，每次循环pop出一个值 然后将二叉树的子节点再放到queue里

在每一次while循环时 嵌套一个for循环，循环长度就是当前queue的长度（这样能保证在for结束后上一层的节点已经被全部移除）。在每次for loop 里 都pop出一个节点，并且将该节点的子节点加到queue里

⚠️每次pop的时候需要从头pop 因为这是一个先进先出的list

当走到最底层的时候已经没有可以放到queue里的节点了 此时queue为空 跳出循环

这道题还需要一组数字来记录每一层一共有多少子节点 以及子节点的总和

```Python
def averageOfLevels(self, root: TreeNode) -> List[float]:
  if not root:
    return []
  queue = collections.deque()
  queue.append(root)
  ans = []
  while queue:
    sum = 0
    count = 0
    for i in range(len(queue)):
      count += 1
      cur = queue.popleft()
      if cur:
        sum += cur.val
      if cur.left:
        queue.append(cur.left)
      if cur.right:
        queue.append(cur.right)
    ans.append(float(sum/count))
  return ans
```



### 513.Find Bottom Left Tree Value (Medium) 得到左下角的节点✅

```html
Input:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

Output:
7
```

这道题也是可以用一个层次遍历来做， 用的是先进先出的queue

只要我们每次把node加到queue里的时候 把右边的节点先加进去，左边的节点后加进去就可以了

⚠️这里说的是最左边的节点 并不一定要是左节点

```python
def findBottomLeftValue(self, root: TreeNode) -> int:
  queue = collections.deque()
  queue.append(root)
  while queue:
    cur = queue.popleft()
    if cur.right:
      queue.append(cur.right)
    if cur.left:
      queue.append(cur.left)
  return cur.val
```



### 144. Binary Tree Preorder Traversal (Medium) 非递归实现二叉树的前序遍历✅

这道题我用了递归（DFS)与非递归(BFS)的方法分别做了一下

非递归的方法用的是一个先进后出的queue

递归的方法是有套路的，记下来就好了, 具体套路我放在了LeetCode笔记里

具体的顺序可以参考下一题的图

```python
def preorderTraversal(self, root: TreeNode) -> List[int]:
  #非递归方法
  if not root:
    return []
  stack = [root]
  ans = []
  while stack:
    cur = stack.pop()
    if cur:
      ans.append(cur.val)
    if cur.right:
      stack.append(cur.right)
    if cur.left:
      stack.append(cur.left)
  return ans

def preorderTraversal(self, root: TreeNode) -> List[int]:
  #递归的方法
  if not root:
    return []
  ans =[]
  def dfs(node):
    if not node:
      return
    ans.append(node.val)
    dfs(node.left)
    dfd(node.right)
  dfs(root)
  return ans
```



### 145. Binary Tree Postorder Traversal (Hard) 非递归实现二叉树的后序遍历✅

套路都是类似的

![](https://leetcode.com/articles/Figures/145_transverse.png)

```python
def postorderTraversal(self, root: TreeNode) -> List[int]:
  # 非递归的方法
  if not root:
    return []
  stack = collections.deque()
  stack.append(root)
  ans = collections.deque()
  while stack:
    cur = stack.pop()
    if cur:
      ans.appendleft(cur.val)
    if cur.left:
      stack.append(cur.left)
    if cur.right:
      stack.append(cur.right)
   return ans

def postorderTraversal(self, root: TreeNode) -> List[int]:  
  #递归的方法
  if not root:
    return []
  ans = []
  def dfs(node):
    if not node:
      return
    dfs(node.left)
    dfs(node.right)
    ans.append(node.val)
  dfs(root)
  return ans
    
  
```



















