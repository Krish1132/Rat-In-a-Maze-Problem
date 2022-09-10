# Rat In a Maze Problem

### Problem - 
The starting position of a rat which is stuck in a maze is given as (0, 0), which is the initial point. The maze is a 0-1 square matrix, where a cell value of '0' represents that the cell cannot be visited and '1' represents that the cell is safe to visit. We have to find all the possible paths by which the rat can reach the position (n - 1, n - 1), that is, the last cell of the matrix. The possible directions in which the rat can move are 'U' (row - 1, column), 'D' (row + 1, column), 'L' (row, column - 1), 'R' (row, column + 1). The output should be sorted in alphabetical order.

---

### Algorithm: 

**Auxillary methods**

*isSafe( )* &rarr; method to determine whether a particular cell can be visited or not
             <br/> A cell can only be visited if it is in-bounds of the the array __((row >= 0 and row < n - 1) and (column >= 0 and column < n))__,
                     the __cell of the maze does not contains 0__ and the cell is __not previously visited__.

*solve( )* &rarr; method to tarverse the maze recursively in all the four possible directions and add the solution paths to the ArrayList
             <br/>Base case - when __row = n - 1 and column = n - 1__, we add the path to the ArrayList and return



Step 1 - Declare the base case <br/>
Step 2 - Mark the current row and column a visited <br/>
Step 3 - recursively call the function for all the four possible directions, if isSafe(next cell) = true
         while calling the functions recursively, pass in the path with the respective direction appended to it <br/>
Step 4 - 
 
---

JAVA logic to solve the "Rat In A Maze" problem using Backtracking



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
