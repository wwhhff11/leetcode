````
// https://leetcode-cn.com/problems/powx-n/
func myPow(x float64, n int) float64 {
    // 当n>0，x^n=x*x*x*x
    // 当n==0，x^0=1
    // 当n<0。x^-n=(1/x)^n
    if n<0 {
        return quick(1/x, -n)
    }
    return quick(x, n)
}

// n>=0
func quick(x float64, n int) float64 {
    if n == 0 {
        return 1.0
    }
    if n == 1 {
        return x
    }
    var half = quick(x, n/2) // 减少一半调用
    if n%2 == 0 { // 偶数
        return half*half
    }
    return half*half*x
}
````