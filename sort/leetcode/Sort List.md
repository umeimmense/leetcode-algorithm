## 题目描述[（link）](https://leetcode-cn.com/problems/sort-list)
给你链表的头结点 head ，请将其按 升序 排列并返回 排序后的链表 。

**进阶：**<br />你可以在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序吗？<br />**示例 1：**<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/126606/1629906460514-2dcd3495-c424-4742-b659-b120253f3558.png#clientId=u0d2719e0-257e-4&from=paste&height=142&id=U3m2U&margin=%5Bobject%20Object%5D&name=image.png&originHeight=284&originWidth=670&originalType=binary&ratio=1&size=52982&status=done&style=none&taskId=u8491439c-af5d-4ae4-aa1a-3277dae17f4&width=335)
> 输入：head = [4,2,1,3]
> 输出：[1,2,3,4]

**示例 2：**<br />![image.png](https://cdn.nlark.com/yuque/0/2021/png/126606/1629906472481-45ba0027-d8c9-473b-a785-e5b0b106c9d6.png#clientId=u0d2719e0-257e-4&from=paste&height=142&id=u72a70c78&margin=%5Bobject%20Object%5D&name=image.png&originHeight=284&originWidth=902&originalType=binary&ratio=1&size=75194&status=done&style=none&taskId=uc3e68209-d05d-4bbd-9dfe-2044be78406&width=451)
> 输入：head = [-1,5,3,4,0]
> 输出：[-1,0,3,4,5]


**示例 3：**
> 输入：head = []
> 输出：[]
> 提示：
> 链表中节点的数目在范围 [0, 5 * 104] 内
> -105 <= Node.val <= 105



## 思路分析及代码实现
这道题考虑时间复杂度更低的排序算法。题目的进阶问题要求达到 O(nlogn) 的时间复杂度和 O(1) 的空间复杂度，时间复杂度是 O(nlogn) 的排序算法包括归并排序、堆排序和快速排序（快速排序的最差时间复杂度是 O(n^2)，其中最适合链表的排序算法是归并排序。

归并排序基于分治算法。最容易想到的实现方式是自顶向下的递归实现，考虑到递归调用的栈空间，自顶向下归并排序的空间复杂度是 O(logn)。如果要达到 O(1) 的空间复杂度，则需要使用自底向上的实现方式。


### 方法一：自顶向下归并排序
对链表自顶向下归并排序的过程如下。

1. 找到链表的中点，以中点为分界，将链表拆分成两个子链表。寻找链表的中点可以使用快慢指针的做法，快指针每次移动 2 步，慢指针每次移动 1 步，当快指针到达链表末尾时，慢指针指向的链表节点即为链表的中点。
1. 对两个子链表分别排序。
1. 将两个排序后的子链表合并，得到完整的排序后的链表。可以使用「21. 合并两个有序链表」的做法，将两个有序的子链表进行合并。

上述过程可以通过递归实现。递归的终止条件是链表的节点个数小于或等于 1，即当链表为空或者链表只包含 1 个节点时，不需要对链表进行拆分和排序。

#### JS版本
```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
const merge = (head1, head2) => {
    const dummyHead = new ListNode(0);
    let temp = dummyHead, temp1 = head1, temp2 = head2;
    while (temp1 !== null && temp2 !== null) {
        if (temp1.val <= temp2.val) {
            temp.next = temp1;
            temp1 = temp1.next;
        } else {
            temp.next = temp2;
            temp2 = temp2.next;
        }
        temp = temp.next;
    }
    if (temp1 !== null) {
        temp.next = temp1;
    } else if (temp2 !== null) {
        temp.next = temp2;
    }
    return dummyHead.next;
}

const toSortList = (head, tail) => {
    if (head === null) {
        return head;
    }
    if (head.next === tail) {
        head.next = null;
        return head;
    }
    let slow = head, fast = head;
    while (fast !== tail) {
        slow = slow.next;
        fast = fast.next;
        if (fast !== tail) {
            fast = fast.next;
        }
    }
    const mid = slow;
    return merge(toSortList(head, mid), toSortList(mid, tail));
}

/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var sortList = function(head) {
    return toSortList(head, null);
};
```

#### GoLang版本
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func merge(head1, head2 *ListNode) *ListNode {
    dummyHead := &ListNode{}
    temp, temp1, temp2 := dummyHead, head1, head2
    for temp1 != nil && temp2 != nil {
        if temp1.Val <= temp2.Val {
            temp.Next = temp1
            temp1 = temp1.Next
        } else {
            temp.Next = temp2
            temp2 = temp2.Next
        }
        temp = temp.Next
    }
    if temp1 != nil {
        temp.Next = temp1
    } else if temp2 != nil {
        temp.Next = temp2
    }
    return dummyHead.Next
}

func sort(head, tail *ListNode) *ListNode {
    if head == nil {
        return head
    }

    if head.Next == tail {
        head.Next = nil
        return head
    }

    slow, fast := head, head
    for fast != tail {
        slow = slow.Next
        fast = fast.Next
        if fast != tail {
            fast = fast.Next
        }
    }

    mid := slow
    return merge(sort(head, mid), sort(mid, tail))
}

func sortList(head *ListNode) *ListNode {
    return sort(head, nil)
}
```

#### 复杂度分析
- 时间复杂度：O(nlogn)，其中 n 是链表的长度。
- 空间复杂度：O(logn)，其中 n 是链表的长度。空间复杂度主要取决于递归调用的栈空间。


### 方法二：自底向上归并排序
使用自底向上的方法实现归并排序，则可以达到 O(1) 的空间复杂度。<br />首先求得链表的长度 length，然后将链表拆分成子链表进行合并。<br />具体做法如下。

1. 用 subLength 表示每次需要排序的子链表的长度，初始时subLength=1。
1. 每次将链表拆分成若干个长度为 subLength 的子链表（最后一个子链表的长度可以小于 subLength），按照每两个子链表一组进行合并，合并后即可得到若干个长度为 subLength×2 的有序子链表（最后一个子链表的长度可以小于 subLength×2）。合并两个子链表仍然使用「21. 合并两个有序链表」的做法。
1. 将subLength 的值加倍，重复第 2 步，对更长的有序子链表进行合并操作，直到有序子链表的长度大于或等于 length，整个链表排序完毕。

如何保证每次合并之后得到的子链表都是有序的呢？可以通过数学归纳法证明。

1. 初始时 subLength=1，每个长度为 11 的子链表都是有序的。
1. 如果每个长度为subLength 的子链表已经有序，合并两个长度为subLength 的有序子链表，得到长度为 subLength×2 的子链表，一定也是有序的。
1. 当最后一个子链表的长度小于subLength 时，该子链表也是有序的，合并两个有序子链表之后得到的子链表一定也是有序的。

因此可以保证最后得到的链表是有序的。

#### JS版本
```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
const merge = (head1, head2) => {
    const dummyHead = new ListNode(0);
    let temp = dummyHead, temp1 = head1, temp2 = head2;
    while (temp1 !== null && temp2 !== null) {
        if (temp1.val <= temp2.val) {
            temp.next = temp1;
            temp1 = temp1.next;
        } else {
            temp.next = temp2;
            temp2 = temp2.next;
        }
        temp = temp.next;
    }
    if (temp1 !== null) {
        temp.next = temp1;
    } else if (temp2 !== null) {
        temp.next = temp2;
    }
    return dummyHead.next;
}

var sortList = function(head) {
    if (head === null) {
        return head;
    }
    let length = 0;
    let node = head;
    while (node !== null) {
        length++;
        node = node.next;
    }
    const dummyHead = new ListNode(0, head);
    for (let subLength = 1; subLength < length; subLength <<= 1) {
        let prev = dummyHead, curr = dummyHead.next;
        while (curr !== null) {
            let head1 = curr;
            for (let i = 1; i < subLength && curr.next !== null; i++) {
                curr = curr.next;
            }
            let head2 = curr.next;
            curr.next = null;
            curr = head2;
            for (let i = 1; i < subLength && curr != null && curr.next !== null; i++) {
                curr = curr.next;
            }
            let next = null;
            if (curr !== null) {
                next = curr.next;
                curr.next = null;
            }
            const merged = merge(head1, head2);
            prev.next = merged;
            while (prev.next !== null) {
                prev = prev.next;
            }
            curr = next;
        }
    }
    return dummyHead.next;
};
```

#### Golang版本
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func merge(head1, head2 *ListNode) *ListNode {
    dummyHead := &ListNode{}
    temp, temp1, temp2 := dummyHead, head1, head2
    for temp1 != nil && temp2 != nil {
        if temp1.Val <= temp2.Val {
            temp.Next = temp1
            temp1 = temp1.Next
        } else {
            temp.Next = temp2
            temp2 = temp2.Next
        }
        temp = temp.Next
    }
    if temp1 != nil {
        temp.Next = temp1
    } else if temp2 != nil {
        temp.Next = temp2
    }
    return dummyHead.Next
}

func sortList(head *ListNode) *ListNode {
    if head == nil {
        return head
    }

    length := 0
    for node := head; node != nil; node = node.Next {
        length++
    }

    dummyHead := &ListNode{Next: head}
    for subLength := 1; subLength < length; subLength <<= 1 {
        prev, cur := dummyHead, dummyHead.Next
        for cur != nil {
            head1 := cur
            for i := 1; i < subLength && cur.Next != nil; i++ {
                cur = cur.Next
            }

            head2 := cur.Next
            cur.Next = nil
            cur = head2
            for i := 1; i < subLength && cur != nil && cur.Next != nil; i++ {
                cur = cur.Next
            }

            var next *ListNode
            if cur != nil {
                next = cur.Next
                cur.Next = nil
            }

            prev.Next = merge(head1, head2)

            for prev.Next != nil {
                prev = prev.Next
            }
            cur = next
        }
    }
    return dummyHead.Next
}

```

#### 复杂度分析

- 时间复杂度：O(nlogn)，其中 n 是链表的长度。
- 空间复杂度：O(1)。

[](https://leetcode-cn.com/problems/sort-list)


