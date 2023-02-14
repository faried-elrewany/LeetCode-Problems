#### first brute force approach

> traverse through the matrix and if you find an element with value 0
> then change all the elements in its row and column to INT_MIN +1
> but dont change the cells with value zero to not affect the other rows and columns then traverse again and change all INT_MIN +1 to 0

```c++
class Solution {
public:
void setZeroes(vector<vector<int>>& matrix) {

  int rows = matrix.size(), cols = matrix[0].size();
  int mn=INT_MIN+1;

  for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
      if (matrix[i][j] == 0) {
  // change the left side of the row
        int ind = i - 1;
          while (ind >= 0) {
              if (matrix[ind][j] != 0) {
                matrix[ind][j] = mn;
                }
                ind--;
            }
  //// change the right side of the row
          ind = i + 1;
          while (ind < rows) {
              if (matrix[ind][j] != 0) {
                matrix[ind][j] = mn;
                }
              ind++;
              }
  // change the top side of the col
          ind = j - 1;
          while (ind >= 0) {
            if (matrix[i][ind] != 0) {
                matrix[i][ind] = mn;
                }
                ind--;
              }

  // change the bottom side of the col
          ind = j + 1;
          while (ind < cols) {
            if (matrix[i][ind] != 0) {
                matrix[i][ind] =mn;
              }
              ind++;
              }
        }
      }
  }
  // traverse and replace all mn values to zeros
  for (int i = 0; i < rows; i++) {
    for (int j = 0; j < cols; j++) {
      if (matrix[i][j] == mn) {
          matrix[i][j] = 0;
      }
    }
  }

      }

  };

```

#### second better approach

> Take two dummy arrays one of size of the row and the other of size of column. Now traverse through the array.If //matrix[i][j]==0 then set dummy1[i]=0(for row) and dummy2[j]=0(for column).Now traverse through the array //again and if dummy1[i]==0 || dummy2[j]==0 then arr[i][j]=0,else continue.

```c++
class Solution {
public:
void setZeroes(vector<vector<int>>& matrix) {
    int rows = matrix.size(), cols = matrix[0].size();
    vector < int > dummy1(rows,-1), dummy2(cols,-1);

    for (int i = 0; i < rows; i++) {
      for (int j = 0; j < cols; j++) {
        if (matrix[i][j] == 0) {
          dummy1[i] = 0;
          dummy2[j] = 0;
        }
      }
    }

    for (int i = 0; i < rows; i++) {
      for (int j = 0; j < cols; j++) {
          if (dummy1[i] == 0 || dummy2[j]==0) {
            matrix[i][j] = 0;
          }
        }
      }
    }
};

```

#### better approach

> Instead of taking two separate dummy arrays, take the first row and column of the matrix as the array for //checking whether the particular column or row has the value 0 or not.Since matrix[0][0] are overlapping.Therefore //take separate variable col0(say) to check if the 0th column has 0 or not and use matrix[0][0] to check if the 0th //row has 0 or not. Now traverse from the last element to the first element and check if matrix[i][0]==0 || //matrix[0][j]==0 and if true set matrix[i][j]=0, else continue.

```c++
class Solution {
public:
void setZeroes(vector<vector<int>>& matrix) {
  int m = matrix.size();
  int n = matrix[0].size();

        bool isFirstRowZero = false;
        bool isFirstColZero = false;

        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) {
                isFirstColZero = true;
                break;
            }
        }

        for (int j = 0; j < n; j++) {
            if (matrix[0][j] == 0) {
                isFirstRowZero = true;
                break;
            }
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }

        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        if (isFirstColZero) {
            for (int i = 0; i < m; i++) {
                matrix[i][0] = 0;
            }
        }

        if (isFirstRowZero) {
            for (int j = 0; j < n; j++) {
                matrix[0][j] = 0;
            }
        }
    }

};

```
