```
func removeDuplicates(nums []int) int {
    var first, cur int = 0, 1
    var length = len(nums)
    var delCount = 0
    for {
        //  fmt.Println("========>", "first", first, "cur", cur, "length", length)
        if cur >= length || first >= length {
            break
        }
        if nums[first] != nums[cur] { // 如果第一个和第二个不一样，都往后移动
            first = cur
            cur = first + 1
            continue
        }
        delCount = 0 // 得到重复个数
        for i := cur+1; i < length; i++ {
            if nums[cur] == nums[i] {
                delCount++
                continue
            }
            break
        }
        if delCount == 0 { // 重复数小于两个，下一次判断
            first += 2
            cur = first + 1
            continue
        }
        // 开始原地删除
        // fmt.Println(1, "nums", nums, "delCount", delCount, "cur", cur, "length", length)
        var length2 = length
        for i := cur+1; i < length2-delCount; i++ {
            nums[i] = nums[i+delCount]
        }
        // fmt.Println(2, "nums", nums, "delCount", delCount, "cur", cur, "length", length)
        length -= delCount
        first += 2
        cur = first + 1
    }
    return length // 返回最终长度
}
```
