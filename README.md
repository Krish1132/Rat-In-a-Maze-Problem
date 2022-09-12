# Rat In a Maze Problem

### Problem - 
The starting position of a rat which is stuck in a maze is given as (0, 0), which is the initial point. The maze is a 0-1 square matrix, where a cell value of '0' represents that the cell cannot be visited and '1' represents that the cell is safe to visit. We have to find all the possible paths by which the rat can reach the position (n - 1, n - 1), that is, the last cell of the matrix. The possible directions in which the rat can move are 'U' (row - 1, column), 'D' (row + 1, column), 'L' (row, column - 1), 'R' (row, column + 1). The output should be sorted in alphabetical order.

---

### Algorithm -

**Auxillary methods**
<ul>
<li> <em>isSafe( )</em> &rarr; method to determine whether a particular cell can be visited or not
             <br/>&emsp;&emsp;&emsp;&ensp;&nbsp;A cell can only be visited if it is in-bounds of the the array <strong>((row >= 0 and row < n - 1) and (column >= 0 and column < n))</strong>,
                     the <strong>cell of the maze does not contains 0</strong> and the cell is <strong>not previously visited</strong>. </li>

<li> <em>solve( )</em> &rarr; method to tarverse the maze recursively in all the four possible directions and add the solution paths to the ArrayList
             <br/>&emsp;&emsp;&emsp;&ensp;&nbsp;Base case - when <strong>row = n - 1 and column = n - 1</strong>, we add the path to the ArrayList and return </li>
</ul>

  *solve( )*<br/>
  Step 1 - Declare the base case <br/>
  Step 2 - Mark the current row and column a visited <br/>
  Step 3 - Recursively call the function for all the four possible directions, if isSafe(next cell) = true<br/>
           &emsp;&emsp;&emsp;&ensp;&nbsp;while calling the functions recursively, pass in the path with the respective direction appended to it <br/>
  Step 4 - At the end we mark visited[row][column] = false when backtracking so that other valid function calls can reuse the path<br/>
  
  *findPath( )* <br/>
  Step 1 - Declare an ArrayList <br/>
  Step 2 - if the starting cell is '0' then return the empty list <br/>
  Step 3 - else declare an empty string 'path' and a 2D boolean array 'visited' to keep track of the path and the visited cell respectively <br/>
  Step 4 - initialize all the positions of the 'visited' array to false <br/>
  Step 5 - Call the method solve and pass the original maze 2D array, its size, the initial starting cell (0, 0), the 'path' empty string, the 'visited' 2D array and the list to store the answer <br/>
  Step 6 - Finally, return the list <br/>
  
  
---

### JAVA logic to solve the "Rat In A Maze" problem using Backtracking -



```
  public static boolean isSafe(int arr[][], int x, int y, int n, boolean visited[][]){
      if(x >= 0 && x < n && y >= 0 && y < n && arr[x][y] == 1 && !visited[x][y]){
          return true;
      }
      return false;
  }

  public static void solve(int arr[][], int x, int y, int n, String path, ArrayList<String> sol, boolean visited[][]){
      if(x == n - 1 && y == n - 1){
          sol.add(path);
          return;
      }
      visited[x][y] = true;
      
      // Down
      if(isSafe(arr, x + 1, y, n, visited)){
          solve(arr, x + 1, y, n, path + "D", sol, visited);
      }    
      
      // Right
      if(isSafe(arr, x, y + 1, n, visited)){
          solve(arr, x, y + 1, n, path + "R", sol, visited);
      }      
      
      // Up
      if(isSafe(arr, x - 1, y, n, visited)){
          solve(arr, x - 1, y, n, path + "U", sol, visited);
      }
      
      // Left
      if(isSafe(arr, x, y - 1, n, visited)){
          solve(arr, x, y - 1, n, path + "L", sol, visited);
      }
      
      visited[x][y] = false; // Backtracking
  }

  public static ArrayList<String> findPath(int[][] m, int n) {
      ArrayList<String> sol = new ArrayList<>();
      if(m[0][0] == 0) return sol;
      String path = "";
      boolean visited[][] = new boolean[n][n];
      for(int i = 0; i < n; i++){
          for(int j = 0; j < n; j++){
              visited[i][j] = false;
          }
      }
      solve(m, 0, 0, n, path, sol, visited);
      return sol;
  }
  ```
  
  ### Time complexity - ###
  
  There are four possible calls from each cell. There worst case time-complexity will be:
  **O(4<sup>n x n</sup>)** = **O(4<sup>n<sup>2</sup></sup>)**
  
  
  ### Space complexity - ###
  
  **O(n<sup>2</sup>)**
