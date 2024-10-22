# Unique Paths II

## https://leetcode.com/problems/unique-paths-ii

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and space is marked as 1 and 0 respectively in the grid.


**Algorithm :**

1. If the first cell i.e. obstacleGrid[0,0] contains 1, this means there is an obstacle in the first cell. 
Hence the robot won't be able to make any move and we would return the number of ways as 0.
Otherwise, if obstacleGrid[0,0] has a 0 originally we set it to 1 and move ahead.

2. Iterate the first row. If a cell originally contains a 1, this means the current cell has an obstacle and shouldn't contribute to any path. Hence, set the value of that cell to 0. Otherwise, set it to the value of previous cell i.e. obstacleGrid[i,j] = obstacleGrid[i,j-1]

3. Iterate the first column. If a cell originally contains a 1, this means the current cell has an obstacle and shouldn't contribute to any path. Hence, set the value of that cell to 0. Otherwise, set it to the value of previous cell i.e. obstacleGrid[i,j] = obstacleGrid[i-1,j]

4. Now, iterate through the array starting from cell obstacleGrid[1,1]. If a cell originally doesn't contain any obstacle then the number of ways of reaching that cell would be the sum of number of ways of reaching the cell above it and number of ways of reaching the cell to the left of it.
 obstacleGrid[i,j] = obstacleGrid[i-1,j] + obstacleGrid[i,j-1]
If a cell contains an obstacle set it to 0 and continue. This is done to make sure it doesn't contribute to any other path.



```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int rows = obstacleGrid.length;
        int cols = obstacleGrid[0].length;
        if(obstacleGrid == null || obstacleGrid[0][0] == 1)
          return 0;

        obstacleGrid[0][0] = 1;
        for(int col = 1; col < cols; col++)
            obstacleGrid[0][col] = obstacleGrid[0][col] == 1 ? 0 : obstacleGrid[0][col-1];   
        for(int row = 1; row < rows; row++) 
            obstacleGrid[row][0] = obstacleGrid[row][0] == 1 ? 0 : obstacleGrid[row-1][0];
            
        for(int row = 1; row < rows; row++) {
            for(int col = 1; col < cols; col++) {
               obstacleGrid[row][col] = obstacleGrid[row][col] == 1 ? 0 :
                                        obstacleGrid[row][col-1] + obstacleGrid[row-1][col];  
            }
        }    
        return obstacleGrid[rows-1][cols-1];  
    }
}
```

# References :

1. https://leetcode.com/problems/unique-paths-ii/solution
