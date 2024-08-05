# placement leetcode
##5/08/24
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
```

#51. N-Queens
## Approach
1.Initialize the Board:
-Create an 𝑁×𝑁 board and initialize all positions with '.' to represent empty spaces.

2.**Use Helper Arrays:**
-Use three helper arrays to keep track of threatened positions:
-leftRow[]: Tracks if a row is occupied by a queen.
-lowerDiagonal[]: Tracks if a descending diagonal (from top-left to bottom-right) is occupied.
-upperDiagonal[]: Tracks if an ascending diagonal (from bottom-left to top-right) is occupied.

3.**Backtracking Function:**
-Implement a recursive function to place queens column by column. For each column, try to place a queen in every row. If a valid position is found, mark the board and auxiliary arrays, then recursively place the next queen. Backtrack if no valid placement is found.
4.**Construct the Solution:**
-Convert the board configuration into a list of strings, where each string represents a row in the board.

## Complexity
-Time Complexity: O(N!)
The time complexity arises from exploring all possible placements of queens, leading to factorial growth with the size of N.
-Space Complexity: 𝑂(\𝑁^2\)
The space complexity includes the storage for the board and auxiliary arrays, as well as the recursion stack.
## Code
```java
class Solution {
    public List<List<String>> solveNQueens(int n) {
         char[][] board = new char[n][n];
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                board[i][j] = '.';
        List < List < String >> res = new ArrayList < List < String >> ();
        int leftRow[] = new int[n];
        int upperDiagonal[] = new int[2 * n - 1];
        int lowerDiagonal[] = new int[2 * n - 1];
        solve(0, board, res, leftRow, lowerDiagonal, upperDiagonal);
        return res;
    }



    static void solve(int col, char[][] board, List < List < String >> res, int leftRow[], int lowerDiagonal[], int upperDiagonal[]) {
        if (col == board.length) {
            res.add(construct(board));
            return;
        }

        for (int row = 0; row < board.length; row++) {
            if (leftRow[row] == 0 && lowerDiagonal[row + col] == 0 && upperDiagonal[board.length - 1 + col - row] == 0) {
                board[row][col] = 'Q';
                leftRow[row] = 1;
                lowerDiagonal[row + col] = 1;
                upperDiagonal[board.length - 1 + col - row] = 1;
                solve(col + 1, board, res, leftRow, lowerDiagonal, upperDiagonal);
                board[row][col] = '.';
                leftRow[row] = 0;
                lowerDiagonal[row + col] = 0;
                upperDiagonal[board.length - 1 + col - row] = 0;
            }
        }
    }


    static List < String > construct(char[][] board) {
        List < String > res = new LinkedList < String > ();
        for (int i = 0; i < board.length; i++) {
            String s = new String(board[i]);
            res.add(s);
        }
        return res;
    }
}
```










