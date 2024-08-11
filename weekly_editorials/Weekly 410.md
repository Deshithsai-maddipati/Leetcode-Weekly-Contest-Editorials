## Snake in Matrix

<details>
<summary>Python</summary>

```python
class Solution:
    def finalPositionOfSnake(self, n: int, commands: List[str]) -> int:
        i, j = 0, 0
        for k in commands:
            if k == "UP":
                i -= 1
            elif k == "DOWN":
                i += 1
            elif k == "RIGHT":
                j += 1
            else:
                j -= 1
                
        return (i * n) + j
```

</details>

<details>
<summary>Cpp</summary>

```cpp
class Solution {
public:
    int finalPositionOfSnake(int n, vector<string>& commands) {
        int i = 0 , j = 0;
        for(string k : commands)
        {
            if(k == "UP")
            {
                i--;
            }
            else if(k == "DOWN")
            {
                i++;
            }
            else if(k == "RIGHT")
            {
                j++;
            }
            else
            {
                j--;
            }
                
        }
        return (i * n) + j;
    }
};
```

</details>

<details>
<summary>Java</summary>

```java
import java.util.List;

class Solution {
    public int finalPositionOfSnake(int n, List<String> commands) {
        int i = 0, j = 0;
        for (String k : commands) {
            if (k.equals("UP")) {
                i--;
            } else if (k.equals("DOWN")) {
                i++;
            } else if (k.equals("RIGHT")) {
                j++;
            } else {
                j--;
            }
        }
        return (i * n) + j;
    }
}

```

</details>

## Count the Number of Good Nodes
<details>
<summary>Python</summary>

```python
class Solution:
    def countGoodNodes(self, edges: List[List[int]]) -> int:
        tree = defaultdict(list)
        for i, j in edges:
            tree[i].append(j)
            tree[j].append(i)
        
        def dfs(node, parent):
            s = 1
            childs = []
            for i in tree[node]:
                if i == parent:
                    continue
                size = dfs(i, node)
                s += size
                childs.append(size)

            if len(set(childs)) <= 1:
                self.good_nodes += 1
            
            return s
        
        self.good_nodes = 0
        dfs(0, -1)
        return self.good_nodes

```

</details>

<details>
<summary>Cpp</summary>

```cpp
class Solution {
public:
    int countGoodNodes(vector<vector<int>>& edges) {
        for (const auto& edge : edges) {
            int u = edge[0];
            int v = edge[1];
            tree[u].push_back(v);
            tree[v].push_back(u);
        }
        
        good_nodes = 0;
        dfs(0, -1); 
        return good_nodes;
    }

private:
    unordered_map<int, vector<int>> tree;
    int good_nodes;
	
    int dfs(int node, int parent) {
        int subtree_size = 1;  
        vector<int> child_sizes;

        for (int child : tree[node]) {
            if (child == parent) {
                continue; 
            }
            int size = dfs(child, node);
            subtree_size += size;  
            child_sizes.push_back(size);  
        }

        if (unordered_set<int>(child_sizes.begin(), child_sizes.end()).size() <= 1) {
            good_nodes++;
        }

        return subtree_size; 
    }
};
```

</details>

<details>
<summary>Java</summary>

```java
import java.util.*;

class Solution {
    private Map<Integer, List<Integer>> tree = new HashMap<>();
    private int goodNodes;

    public int countGoodNodes(int[][] edges) {
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            tree.computeIfAbsent(u, k -> new ArrayList<>()).add(v);
            tree.computeIfAbsent(v, k -> new ArrayList<>()).add(u);
        }
        
        goodNodes = 0;
        dfs(0, -1);
        return goodNodes;
    }

    private int dfs(int node, int parent) {
        int subtreeSize = 1;  
        List<Integer> childSizes = new ArrayList<>();

        for (int child : tree.get(node)) {
            if (child == parent) {
                continue; 
            }
            int size = dfs(child, node);
            subtreeSize += size;  
            childSizes.add(size);  
        }

        if (new HashSet<>(childSizes).size() <= 1) {
            goodNodes++;
        }

        return subtreeSize; 
    }
}

```

</details>

## Find the Count of Monotonic Pairs I

<details>
<summary>Python</summary>

```python
    def countOfPairs(self, A: List[int]) -> int:
        mod = 10 ** 9 + 7
        n, m = len(A), max(A) + 1
        dp, dp2 = [1] * m, [0] * m
        for i in range(1, n):
            d = max(0, A[i] - A[i - 1])
            for j in range(d, A[i] + 1):
                dp2[j] = (dp2[j - 1] + dp[j - d]) % mod
            dp, dp2 = dp2, [0] * m
        return sum(dp) % mod

```

</details>

<details>
<summary>Cpp</summary>

```cpp


    int countOfPairs(vector<int>& A) {
        int n = A.size(), m = 1001, mod = 1e9 + 7;
        vector<int> dp(m, 1);

        for (int i = 1; i < n; ++i) {
            int d = max(0, A[i] - A[i - 1]);
            vector<int> dp2(m, 0);
            for (int j = d; j < A[i] + 1; ++j) {
                dp2[j] = ((j > 0 ? dp2[j - 1] : 0) + dp[j - d]) % mod;
            }
            swap(dp, dp2);
        }

        int res = 0;
        for (int j = 0; j <= A[n - 1]; ++j)
            res = (res + dp[j]) % mod;
        return res;
    }

```

</details>

<details>
<summary>Java</summary>

```java
    public int countOfPairs(int[] A) {
        int n = A.length, m = 1001, mod = 1000000007, dp[] = new int[m];
        Arrays.fill(dp, 1);

        for (int i = 1; i < n; ++i) {
            int d = Math.max(0, A[i] - A[i - 1]), dp2[] = new int[m];
            for (int j = d; j < A[i] + 1; ++j) {
                dp2[j] = ((j > 0 ? dp2[j - 1] : 0) + dp[j - d]) % mod;
            }
            dp = dp2;
        }

        int res = 0;
        for (int j = 0; j <= A[n - 1]; ++j)
            res = (res + dp[j]) % mod;
        return res;
    }

```

</details>

## Find the Count of Monotonic Pairs II

<details>
<summary>Python</summary>

```python

    def countOfPairs(self, A: List[int]) -> int:
        mod = 10 ** 9 + 7
        n, m = len(A), max(A) + 1
        dp, dp2 = [1] * m, [0] * m
        for i in range(1, n):
            d = max(0, A[i] - A[i - 1])
            for j in range(d, A[i] + 1):
                dp2[j] = (dp2[j - 1] + dp[j - d]) % mod
            dp, dp2 = dp2, [0] * m
        return sum(dp) % mod
```
</details>

<details>
<summary>Cpp</summary>

```cpp

 class Solution {
public:
    int countOfPairs(vector<int>& nums) {
        int n = nums.size(), m = 1001, mod = 1e9 + 7;
        vector<int> dp(m, 1);

        for (int i = 1; i < n; ++i) {
            int d = max(0, nums[i] - nums[i - 1]);
            vector<int> dp2(m, 0);
            for (int j = d; j < nums[i] + 1; ++j) {
                dp2[j] = ((j > 0 ? dp2[j - 1] : 0) + dp[j - d]) % mod;
            }
            swap(dp, dp2);
        }

        int res = 0;
        for (int j = 0; j <= nums[n - 1]; ++j)
            res = (res + dp[j]) % mod;
        return res;
    
    }
};
```

</details>

<details>
<summary>Java</summary>

```java
 
 import java.util.Arrays;

class Solution {
    public int countOfPairs(int[] nums) {
        int n = nums.length, m = 1001, mod = (int)1e9 + 7;
        int[] dp = new int[m];
        Arrays.fill(dp, 1);

        for (int i = 1; i < n; ++i) {
            int d = Math.max(0, nums[i] - nums[i - 1]);
            int[] dp2 = new int[m];
            for (int j = d; j < nums[i] + 1; ++j) {
                dp2[j] = ((j > 0 ? dp2[j - 1] : 0) + dp[j - d]) % mod;
            }
            dp = dp2;
        }

        int res = 0;
        for (int j = 0; j <= nums[n - 1]; ++j)
            res = (res + dp[j]) % mod;
        return res;
    }
}
```

</details>
