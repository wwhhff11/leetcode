````go
func uniquePathsWithObstacles(obstacleGrid [][]int) int {
    var m = len(obstacleGrid)
    var n = len(obstacleGrid[0])

    // 一期的代码
    var dp = make([][]int, m, m)
    for i := 0; i < m; i++ {
        dp[i] = make([]int, n, n)
    }
    for i := 0; i < m; i++ {
        if obstacleGrid[i][0] == 1 {
            break
        }
        dp[i][0] = 1
    }
    for j := 0; j < n; j++ {
        if obstacleGrid[0][j] == 1 {
            break
        }
        dp[0][j] = 1
    }
    for i := 1; i < m; i++ {
        for j := 1; j < n; j++ {
            dp[i][j] = func () int {
                if obstacleGrid[i][j] == 1 {
                    return 0
                }
                var sum int
                if obstacleGrid[i][j-1] == 0 {
                    sum += dp[i][j-1]
                }
                if obstacleGrid[i-1][j] == 0 {
                    sum += dp[i-1][j]
                }
                return sum
            }()
        }
    }
    return dp[m-1][n-1]
}
````