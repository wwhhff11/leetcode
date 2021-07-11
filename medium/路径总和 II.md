````go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func pathSum(root *TreeNode, targetSum int) [][]int {
    var res = make([][]int, 0, 0)
    var cur = make([]int, 0, 0)
    dfs(root, targetSum, cur, &res)
    // for i := range res {
    //     fmt.Println(res[i])
    // }
    return res
}

func dfs(root *TreeNode, targetSum int, cur []int, res *[][]int) {
    if root == nil {
        return
    }
    if root.Left == nil && root.Right == nil { // 叶子节点
        if root.Val == targetSum {
            next := deepCopy(cur)
            next = append(next, root.Val)
            (*res) = append((*res), next) // 加入结果
        }
        return
    } else { // 非叶子节点
        if root.Left != nil {
            next := deepCopy(cur)
            next = append(next, root.Val)
            dfs(root.Left, targetSum-root.Val, next, res)
        }
        if root.Right != nil {
            next := deepCopy(cur)
            next = append(next, root.Val)
            dfs(root.Right, targetSum-root.Val, next, res)
        }
    }    
}

func deepCopy(arr []int) []int {
    var res = make([]int, 0, len(arr))
    for i := range arr {
        res = append(res, arr[i])
    }
    return res
}
````