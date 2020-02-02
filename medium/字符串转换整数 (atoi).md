````go
func myAtoi(str string) int {
    var blankPrefixFilter = func(src string) string { // 空格前缀过滤
        var res = make([]byte, 0, len(src))
        var stopFilter bool
        for i := range src{
            if src[i] == byte(' ') && !stopFilter {
                continue
            }
            res = append(res, src[i])
            stopFilter = true // 数字后面的空格不能过滤
        }
        return string(res)
    }
    var continuousNumFilter = func(src string) string { // 截取连续数字
        var res = make([]byte, 0, len(src))
        var isPositive bool = true
        if src[0] == byte('-') {
            isPositive = false
            src = src[1:] // 截取字符串
        } else if src[0] == byte('+') { // 当我们寻找到的第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字组合起来，尼玛还有加号
            src = src[1:] // 截取字符串
        }
        for i := range src {
            if src[i] < byte('0') || src[i] > byte('9') {
                break
            }
            res = append(res, src[i])
        }
        if !isPositive {
            return "-" + string(res)
        }
        return string(res)
    }
    str = blankPrefixFilter(str)
    if str == "" {
        return 0
    }
    str = continuousNumFilter(str)
    if str == "" {
        return 0
    }

    // 同整数反转处理一样判断精度：https://github.com/wwhhff11/leetcode/blob/master/easy/%E6%95%B4%E6%95%B0%E5%8F%8D%E8%BD%AC.md
    
    var i64res, _ = strconv.ParseInt(str, 10, 64) 
    if int64(int32(i64res)) != i64res { // 溢出
        if i64res > 0 { // 根据题目适配结果
            return 2147483647
        }
        return -2147483648
    }
    return int(i64res)
}
````