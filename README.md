# placement leetcode
# 43.Rotate an \( n \times n \) Matrix by 90 Degrees Clockwise

## Approach
1. **Transpose the Matrix**: Iterate through the matrix, and for each element above the main diagonal, swap it with the corresponding element below the diagonal.
2. **Reverse Each Row**: After transposing, reverse the elements of each row to complete the 90-degree rotation.

## Complexity
- **Time complexity**: \( O(n^2) \)
  - Transposing the matrix and reversing each row both involve iterating over the entire matrix, leading to a quadratic time complexity.
- **Space complexity**: \( O(1) \)
  - The operations are performed in place without using additional data structures that grow with the input size.
## Code
```java
class Solution 
{
    public void rotate(int[][] matrix)
    {
        int n = matrix.length;
        // Transpose the matrix
        for(int i = 0; i < n - 1; i++)
        {
            for(int j = i + 1; j < n; j++)
            {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        // Reverse each row
        for(int i = 0; i < n; i++)
        {
            int l = 0, r = n - 1;
            while(l < r)
            {
                int temp = matrix[i][l];
                matrix[i][l] = matrix[i][r];
                matrix[i][r] = temp;
                l++;
                r--;
            }
        }
    }
}
