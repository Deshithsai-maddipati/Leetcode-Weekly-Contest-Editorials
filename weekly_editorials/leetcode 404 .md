## Maximum height of a triangle

<details>
<summary>Python</summary>

```python
# Python code
class Solution:
    def maxHeightOfTriangle(self, red: int, blue: int) -> int:
        return max(self.helper(red, blue), self.helper(blue, red))
    
    def helper(self, red: int, blue: int) -> int:
        h = 0
        i = 1

        while True:
            if i % 2 == 1:
                if red >= i:
                    red -= i
                else:
                    break
            else:
                if blue >= i:
                    blue -= i
                else:
                    break
            h += 1
            i += 1
        
        return h


```

</details>

<details>
<summary>Cpp</summary>

```cpp
 class Solution {
public:
    int maxHeightOfTriangle(int red, int blue) {
        return std::max(helper(red, blue), helper(blue, red));
    }

private:
    int helper(int red, int blue) {
        int h = 0;
        int i = 1;

        while (true) {
            if (i % 2 == 1) {
                if (red >= i) {
                    red -= i;
                } else {
                    break;
                }
            } else {
                if (blue >= i) {
                    blue -= i;
                } else {
                    break;
                }
            }
            h++;
            i++;
        }

        return h;
    }
};


```

</details>

<details>
<summary>Java</summary>

```java
class Solution {
    public int maxHeightOfTriangle(int red, int blue) {
        return Math.max(helper(red, blue), helper(blue, red));
    }

    private int helper(int red, int blue) {
        int h = 0;
        int i = 1;

        while (true) {
            if (i % 2 == 1) {
                if (red >= i) {
                    red -= i;
                } else {
                    break;
                }
            } else {
                if (blue >= i) {
                    blue -= i;
                } else {
                    break;
                }
            }
            h++;
            i++;
        }

        return h;
    }
} 



```

</details>

## find the maximum length of a valid subsequence 1

<details>
<summary>Python</summary>

```python
class Solution:
    def minOperations(self, nums):
        n = len(nums)
        i, j = 0, 2
        ans = 0
        while j < n:
            if nums[i] == 0:
                ans += 1
                for k in range(i, i + 3):
                    nums[k] = 1 if nums[k] == 0 else 0
            i += 1
            j += 1
        for i in range(n):
            if nums[i] == 0:
                return -1
        return ansclass Solution:
    def sameParity(self, nums: list[int]) -> int:
        n = len(nums)
        
        even = [0] * n
        if nums[0] % 2 == 0:
            even[0] = 1
        
        for i in range(1, n):
            val = nums[i]
            if val % 2 == 1:
                even[i] = even[i - 1]
            else:
                even[i] = even[i - 1] + 1
        
        odd = [0] * n
        if nums[0] % 2 == 1:
            odd[0] = 1
        
        for i in range(1, n):
            val = nums[i]
            if val % 2 == 0:
                odd[i] = odd[i - 1]
            else:
                odd[i] = odd[i - 1] + 1
        
        return max(even[n - 1], odd[n - 1])
    
    def alternatingParity(self, nums: list[int]) -> int:
        n = len(nums)
        
        even = [0] * n
        odd = [0] * n
        
        if nums[0] % 2 == 0:
            even[0] = 1
        if nums[0] % 2 == 1:
            odd[0] = 1
        
        for i in range(1, n):
            val = nums[i]
            if val % 2 == 0:
                even[i] = 1 + odd[i - 1]
                odd[i] = odd[i - 1]
            else:
                odd[i] = 1 + even[i - 1]
                even[i] = even[i - 1]
        
        return max(even[n - 1], odd[n - 1])
    
    def maximumLength(self, nums: list[int]) -> int:
        return max(self.sameParity(nums), self.alternatingParity(nums))



```

</details>

<details>
<summary>Cpp</summary>

```cpp
class Solution {
public:
    
    int sameParity(vector<int>& nums) {
        int n = nums.size();
        
        vector<int> even(n, 0);
        if (nums[0] % 2 == 0) even[0] = 1;
        
        for (int i = 1; i < n; i++) {
            int val = nums[i];
            
            if (val % 2 == 1) {
                even[i] = even[i - 1];
            } else {
                even[i] = even[i - 1] + 1;
            }
        }
        
        vector<int> odd(n, 0);
        if (nums[0] % 2 == 1) odd[0] = 1;
        
        for (int i = 1; i < n; i++) {
            int val = nums[i];
            if (val % 2 == 0) {
                odd[i] = odd[i - 1];
            } else {
                odd[i] = odd[i - 1] + 1;
            }
        }
        
        return max(even[n - 1], odd[n - 1]);
    }
    
    int alternatingParity(vector<int>& nums) {
        int n = nums.size();
        
        vector<int> even(n, 0);
        vector<int> odd(n, 0);
        
        if (nums[0] % 2 == 0) even[0] = 1;
        if (nums[0] % 2 == 1) odd[0] = 1;
        
        for (int i = 1; i < n; i++) {
            int val = nums[i];
            
            if (val % 2 == 0) {
                even[i] = 1 + odd[i - 1];
                odd[i] = odd[i - 1];
            } else {
                odd[i] = 1 + even[i - 1];
                even[i] = even[i - 1];
            }
        }
        
        return max(even[n - 1], odd[n - 1]);
    }
    
    int maximumLength(vector<int>& nums) {
        return max(sameParity(nums), alternatingParity(nums));
    }
};



```

</details>

<details>
<summary>Java</summary>

```java
// Java code
class Solution {
    
    public int sameParity(int[] nums) {
        int n = nums.length;
        
        int[] even = new int[n];
        if (nums[0] % 2 == 0) even[0] = 1;
        
        for (int i = 1; i < n; i++) {
            int val = nums[i];
            
            if (val % 2 == 1) {
                even[i] = even[i - 1];
            } else {
                even[i] = even[i - 1] + 1;
            }
        }
        
        int[] odd = new int[n];
        if (nums[0] % 2 == 1) odd[0] = 1;
        
        for (int i = 1; i < n; i++) {
            int val = nums[i];
            if (val % 2 == 0) {
                odd[i] = odd[i - 1];
            } else {
                odd[i] = odd[i - 1] + 1;
            }
        }
        
        return Math.max(even[n - 1], odd[n - 1]);
    }
    
    public int alternatingParity(int[] nums) {
        int n = nums.length;
        
        int[] even = new int[n];
        int[] odd = new int[n];
        
        if (nums[0] % 2 == 0) even[0] = 1;
        if (nums[0] % 2 == 1) odd[0] = 1;
        
        for (int i = 1; i < n; i++) {
            int val = nums[i];
            
            if (val % 2 == 0) {
                even[i] = 1 + odd[i - 1];
                odd[i] = odd[i - 1];
            } else {
                odd[i] = 1 + even[i - 1];
                even[i] = even[i - 1];
            }
        }
        
        return Math.max(even[n - 1], odd[n - 1]);
    }
    
    public int maximumLength(int[] nums) {
        return Math.max(sameParity(nums), alternatingParity(nums));
    }
}





```

</details>

## Find the length of valid subsequence 2

<details>
<summary>Python</summary>

```python
class Solution:
    def maximumLength(self, nums: list[int], k: int) -> int:
        dp = [[0] * k for _ in range(k)]
        maxi = 1
        for num in nums:
            currNum = num % k
            for mod in range(k):
                prevNum = (mod - currNum + k) % k
                dp[currNum][mod] = max(dp[currNum][mod], 1 + dp[prevNum][mod])
                maxi = max(maxi, dp[currNum][mod])
        return maxi


```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <vector>

class Solution {
public:
    int maximumLength(vector<int>& nums, int k) {
        vector<vector<int>> dp(k, vector<int>(k, 0));
        int maxi = 1;
        for (int num : nums) {
            int currNum = num % k;
            for (int mod = 0; mod < k; mod++) {
                int prevNum = (mod - currNum + k) % k;
                dp[currNum][mod] = max(dp[currNum][mod], 1 + dp[prevNum][mod]);
                maxi = max(maxi, dp[currNum][mod]);
            }
        }
        return maxi;
    }
};


```

</details>

<details>
<summary>Java</summary>

```java
class Solution {
    public int maximumLength(int[] nums, int k) {
        int[][] dp = new int[k][k];
        int maxi = 1;
        for (int num : nums) {
            int currNum = num % k;
            for (int mod = 0; mod < k; mod++) {
                int prevNum = (mod - currNum + k) % k;
                dp[currNum][mod] = Math.max(dp[currNum][mod], 1 + dp[prevNum][mod]);
                maxi = Math.max(maxi, dp[currNum][mod]);
            }
        }
        return maxi;
    }
}



```

</details>

## find maximum diameter of a tree

<details>
<summary>Python</summary>

```python
class Solution:
    def solve(self, adj, st, farn):
        n = len(adj)
        farn[0] = st
        dis = [-1] * n
        self.helper(adj, st, 0, farn, dis)
        return dis[farn[0]]

    def helper(self, dp, node, distance, farn, dis):
        dis[node] = distance
        if distance > dis[farn[0]]:
            farn[0] = node
        for it in dp[node]:
            if dis[it] == -1:
                self.helper(dp, it, distance + 1, farn, dis)

    def minimumDiameterAfterMerge(self, nums1, nums2):
        n = len(nums1)
        m = len(nums2)
        adj1 = [[] for _ in range(n + 1)]
        adj2 = [[] for _ in range(m + 1)]
        for it in nums1:
            adj1[it[1]].append(it[0])
            adj1[it[0]].append(it[1])
        for it in nums2:
            adj2[it[1]].append(it[0])
            adj2[it[0]].append(it[1])

        far1 = [0]
        self.solve(adj1, 0, far1)
        diameter1 = self.solve(adj1, far1[0], far1)

        far2 = [0]
        self.solve(adj2, 0, far2)
        diameter2 = self.solve(adj2, far2[0], far2)

        return max((diameter1 + 1) // 2 + (diameter2 + 1) // 2 + 1, diameter1, diameter2)

```

</details>

<details>
<summary>Cpp</summary>

```cpp
class Solution
{
public:
    int solve(vector<vector<int>> &adj, int st, int &farn)
    {
        int n = adj.size();
        farn = st;
        vector<int> dis(n, -1);
        helper(adj, st, 0, farn, dis);
        return dis[farn];
    }

    void helper(vector<vector<int>> &dp, int node, int distance, int &farn, vector<int> &dis)
    {
        dis[node] = distance;
        if (distance > dis[farn])
            farn = node;
        for (auto it : dp[node])
            if (dis[it] == -1)
                helper(dp, it, distance + 1, farn, dis);
    }
    int minimumDiameterAfterMerge(vector<vector<int>> &nums1, vector<vector<int>> &nums2)
    {
        int n = nums1.size();
        int m = nums2.size();
        vector<vector<int>> adj1(n + 1);
        vector<vector<int>> adj2(m + 1);
        for (auto &it : nums1)
        {
            adj1[it[1]].push_back(it[0]);
            adj1[it[0]].push_back(it[1]);
        }
        for (auto &it : nums2)
        {
            adj2[it[1]].push_back(it[0]);
            adj2[it[0]].push_back(it[1]);
        }

        int far1 = 0;
        solve(adj1, 0, far1);
        int diameter1 = solve(adj1, far1, far1);

        int far2 = 0;
        solve(adj2, 0, far2);
        int diameter2 = solve(adj2, far2, far2);

        return max({(diameter1 + 1) / 2 + (diameter2 + 1) / 2 + 1, diameter1, diameter2});
    }
};


```

</details>

<details>
<summary>Java</summary>

```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int solve(List<List<Integer>> adj, int st, int[] farn) {
        int n = adj.size();
        farn[0] = st;
        int[] dis = new int[n];
        for (int i = 0; i < n; i++) dis[i] = -1;
        helper(adj, st, 0, farn, dis);
        return dis[farn[0]];
    }

    public void helper(List<List<Integer>> dp, int node, int distance, int[] farn, int[] dis) {
        dis[node] = distance;
        if (distance > dis[farn[0]]) farn[0] = node;
        for (int it : dp.get(node)) {
            if (dis[it] == -1) helper(dp, it, distance + 1, farn, dis);
        }
    }

    public int minimumDiameterAfterMerge(List<List<Integer>> nums1, List<List<Integer>> nums2) {
        int n = nums1.size();
        int m = nums2.size();
        List<List<Integer>> adj1 = new ArrayList<>(n + 1);
        List<List<Integer>> adj2 = new ArrayList<>(m + 1);
        for (int i = 0; i <= n; i++) adj1.add(new ArrayList<>());
        for (int i = 0; i <= m; i++) adj2.add(new ArrayList<>());
        for (List<Integer> it : nums1) {
            adj1.get(it.get(1)).add(it.get(0));
            adj1.get(it.get(0)).add(it.get(1));
        }
        for (List<Integer> it : nums2) {
            adj2.get(it.get(1)).add(it.get(0));
            adj2.get(it.get(0)).add(it.get(1));
        }

        int[] far1 = new int[1];
        solve(adj1, 0, far1);
        int diameter1 = solve(adj1, far1[0], far1);

        int[] far2 = new int[1];
        solve(adj2, 0, far2);
        int diameter2 = solve(adj2, far2[0], far2);

        return Math.max((diameter1 + 1) / 2 + (diameter2 + 1) / 2 + 1, Math.max(diameter1, diameter2));
    }
}


```

</details>

