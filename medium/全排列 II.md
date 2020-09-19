```go
// https://leetcode-cn.com/problems/permutations-ii/
func permuteUnique(nums []int) [][]int {
    sort.Ints(nums) // 排序
    var vis = make([]int, len(nums))
    var arr = make([]int, len(nums))
    var res = make([][]int, 0, 1000)
    // fmt.Printf("11%p %p\n",&res,vis)
    dfs(nums, 0, vis, &res, arr)
    return res
}

// res [][]int值拷贝，为什么？不是slice类型么?
func dfs(nums []int, count int, vis []int, res *[][]int, arr []int) {
    // fmt.Printf("22%p %p\n",res,vis)
    if count == len(nums) { // 得到结果
        // fmt.Println(arr)
        // copy
        var arr2 = make([]int, len(nums))
        copy(arr2, arr)
        // fmt.Printf("---%p\n",&res)
        // fmt.Printf("===%p\n",&res)
        *res = append(*res, arr2) // append 会产生新对象，所以这里必须使用指针，修改底下数据
        return
    }
    var length = len(nums)
    for i := 0; i < length; i++ {

        // 已经访问过
        if vis[i] == 1 {
            continue
        }

        vis[i] = 1
        arr[count] = nums[i]
        dfs(nums, count+1, vis, res, arr)
        arr[count] = 0
        vis[i] = 0 // 同上

        // 已经选择了此元素，当前状态转移下一个状态选取元素，不能取相同，移动到下个不重复的位置
        var j = i+1
        for j < length && nums[j] == nums[i] {
            j++
        }
        i = j-1
    }
}
```
