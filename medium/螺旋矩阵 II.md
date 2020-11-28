````
func generateMatrix(n int) [][]int {
    var res = make([][]int, n)
    var vis = make([][]int, n)
    for i := 0; i < n; i++ {
        res[i] = make([]int, n)
        vis[i] = make([]int, n)
    }
    var num = 1
    var x, y = 0, 0
    for {
        var i, j = x, y
        // 1,2,3
        for ; j < n-y; j++ {
            if vis[i][j] == 1 {
                // fmt.Println("1111:",i,j,num)
                return res
            }
            res[i][j] = num
            num++ 
            vis[i][j] = 1
        }
        // 4,5
        j--
        i++
        for ; i < n-x; i++ {
            if vis[i][j] == 1 {
                //  fmt.Println("2222:",i,j,num)
                return res
            }
            res[i][j] = num
            num++ 
            vis[i][j] = 1
        } 
        // 6,7
        i--
        j--
        for ; j >= y; j-- {
            if vis[i][j] == 1 {
                //  fmt.Println("3333:",i,j,num)
                return res
            }
            res[i][j] = num
            num++ 
            vis[i][j] = 1
        }
        // 8
        j++
        i--
        for ; i > x; i-- {
            if vis[i][j] == 1 {
                //  fmt.Println("4444:",i,j,num)
                return res
            }
            res[i][j] = num
            num++ 
            vis[i][j] = 1
        }
        x++
        y++
        if x >= n || y >= n {
            // fmt.Println("5555:",i,j,num)
            break
        }
    }
    return res
}
````