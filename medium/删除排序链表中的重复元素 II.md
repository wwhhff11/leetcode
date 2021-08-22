```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteDuplicates(head *ListNode) *ListNode {
    if head == nil || head.Next == nil { // 如果只有一个节点，直接返回
        return head
    }
    var ptr, pre *ListNode = head, nil // 指针
    for {
        if ptr == nil || ptr.Next == nil { // 已经到最后了
            break
        }
        if ptr.Val != ptr.Next.Val { // 相临两个节点不相同
            pre = ptr
            ptr = ptr.Next // 都向后移动
            continue
        }
        // 相临两个节点相同
        ptr2, hasMore := func() (*ListNode, bool) {
            var ptr2 = ptr.Next
            for {
                if ptr2 == nil {
                    return nil, false
                }
                if ptr2.Val != ptr.Val { // 直到出现不同的节点
                    return ptr2, true
                }
                ptr2 = ptr2.Next
            }
            return nil, false
        }()
        // 删除相同节点
        if pre == nil { // 说明第一个已经重复了
            head = ptr2
        } else {
            pre.Next = ptr2
        }
        ptr = ptr2
        if !hasMore { // 已经遍历完成了
            break
        }
    }
    return head
}
```
