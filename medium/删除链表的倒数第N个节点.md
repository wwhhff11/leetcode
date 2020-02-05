````go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
 // 参考：https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/
func removeNthFromEnd(head *ListNode, n int) *ListNode {
    // 解法思路：
    // 1. 先求长度再遍历删除结点
    // 2. 双指针，一个从首结点开始遍历，一个从首结点后n个开始遍历，当后面的结点到达尾部时，前一个结点就是倒数第n个结点的前驱结点

    if n == 1 { // 尾结点
        if head.Next == nil { // 只有一个结点
            return nil
        }
        // 删除最后的结点
        var ptr *ListNode = head
        for {
            if ptr.Next.Next == nil {
                ptr.Next = nil
                break
            }
            ptr = ptr.Next
        }
        return head
    }

    // 初始化指针
    var ptr1, ptr2 *ListNode = head, head
    for i := 0; i < n; i++ {
        ptr2 = ptr2.Next
    }

    if ptr2 == nil && n > 1 { // 首结点
        return head.Next
    }

    // 开始遍历
    for {
        if ptr2.Next == nil {
            // 移动到尾部了
            ptr1.Next = ptr1.Next.Next
            break
        }
        ptr2 = ptr2.Next
        ptr1 = ptr1.Next
    }
    return head
}
````