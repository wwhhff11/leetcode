```go
// https://leetcode-cn.com/problems/implement-strstr/
// https://www.jianshu.com/p/2e6eb7386cd3
func strStr(haystack string, needle string) int {
    if len(haystack) < len(needle) {
        return -1
    }
    if needle == "" {
        return 0
    }
    var index4Sunday = func(src, sub string) int {
        // 初始化move数组，o(N)
        var move = make([]int, 0, len(src))
        for i := range src {
            if src[i] == sub[0] {
                move = append(move, i)
            }
        }
        // o(N*M)，N是move数组大小
        for i := range move {
            var length = len(src)
            var ok = func(idx int) (bool) {
                for j := range sub {
                    if idx < length && sub[j] == src[idx] {
                        idx++
                        continue // 一致
                    }
                    return false
                }
                return true
            }(move[i])
            if ok { // 匹配不成功
                return move[i]
            }
        }
        return -1
    }
    return index4Sunday(haystack, needle)
}
```
