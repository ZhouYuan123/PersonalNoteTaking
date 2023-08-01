# 数据结构与算法

程序 = 数据机构 + 算法

## 1. 线性结构

顺序存储结构，链式存储结构。

### 1.1 稀疏数组

Sparse Array:  一般使用在一个二维数组存储着大量无效数据的场景中。

- 第一行记录二维数组的行数，列数，以及有效数据的个数
- 其他行记录每个有效数据所在的行数，列数，以及值

<img src="../imgs/algorithm/sparsearray.jpg" alt="稀疏数组" style="zoom:80%;" />

### 1.2 队列

队列是一个有序列表，可以用数组或是链表来实现。

遵循先入先出的原则。

### 1.3 链表

**Linked List：**

1. 链表是以节点的方式来存储
2. 每个节点包含 data域，next域: 指向下一个节点
3. 链表的各个节点不一定是连续存储.
4. 带头节点或者不带

#### 1.3.1 单向链表

1. 单向链表 **(Singly Linked List)** ，查找的方向只能是一个方向，而双向链表可以向前或者向后查找。
2. 单向链表不能自我删除，需要靠辅助节点，而双向链表，则可以自我删除。(辅助节点通常是指向前一个节点)

**头插法：**

```java
class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
    }
}

public class Main {
    public static void main(String[] args) {
        // 创建一个空链表
        ListNode head = null;

        // 使用头插法向链表中插入新节点
        for (int i = 1; i <= 5; i++) {
            ListNode newNode = new ListNode(i);
            newNode.next = head; // 将新节点的下一个指针指向当前头节点
            head = newNode; // 更新链表的头节点
        }
    }
}
```

<font color=blue>**单向环形链表**</font>

约瑟夫问题 (Josephus problem)

#### 1.3.2 双向链表

**(Doubly Linked List)** ： 可以自我删除。



## 2. 非线性结构