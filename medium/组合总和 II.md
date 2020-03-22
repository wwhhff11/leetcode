```go
// https://leetcode-cn.com/problems/combination-sum-ii/
func dfs(candidates []int, target int, begin int, curArr []int, delta int, res *[][]int) {
    if delta == 0 { // 剩余为0
        *res = append(*res, curArr) // 找到一个结果
        return
    }

    var length = len(candidates)
    var vis = make(map[int]bool, length) // 每一轮搜索保证只搜索同一个数字一次
    for i := begin ;i < length; i++ {
        if delta < candidates[i] { // 比delta大，没必要再搜索下去了，因为肯定不满足条件，剪枝
            break
        }
        if val, ok := vis[candidates[i]]; ok && val {
            continue // 已经搜过
        }
        vis[candidates[i]] = true

        // begin是i，保证可重复
        var copyArr = make([]int, 0, len(curArr)+1)
        copyArr = append(copyArr, curArr...)
        copyArr = append(copyArr, candidates[i])
        dfs(candidates, target, i+1, copyArr, delta-candidates[i], res)
    }
}

func combinationSum2(candidates []int, target int) [][]int {
    // 排序，方便剪枝
    sort.Ints(candidates)
    // 无重复元素，所以不用担心不同元素去重问题
    var res = make([][]int, 0, 0)
    dfs(candidates, target, 0, []int{}, target, &res)
    return res
}
```
