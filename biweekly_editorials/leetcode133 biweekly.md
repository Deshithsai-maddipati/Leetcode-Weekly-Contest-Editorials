## Find Minimum Operations to Make All Elements Divisible by Three

<details>
<summary>Python</summary>

```python
# Python code
class Solution:
    def minimumOperations(self, nums):
        ans = 0
        for num in nums:
            if num % 3 == 0:
                continue
            ans += 1
        return ans


```

</details>

<details>
<summary>Cpp</summary>

```cpp
   #include <vector>

class Solution {
public:
    int minimumOperations(std::vector<int>& nums) {
        int ans = 0;
        // Iterate through each element in the nums vector
        for (int i = 0; i < nums.size(); i++) {
            // If the current element is divisible by 3, skip to the next iteration
            if (nums[i] % 3 == 0) continue;
            // Increment the answer counter if the current element is not divisible by 3
            ans++;
        }
        // Return the final count of elements that are not divisible by 3
        return ans;
    }
};

```

</details>

<details>
<summary>Java</summary>

```java
import java.util.List;

public class Solution {
    public int minimumOperations(List<Integer> nums) {
        int ans = 0;
        for (int num : nums) {
            if (num % 3 == 0) {
                continue;
            }
            ans++;
        }
        return ans;
    }
}



```

</details>

## Minimum operations to Make Binary Array elements Equal to 1

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
        return ans


```

</details>

<details>
<summary>Cpp</summary>

```cpp
class Solution {
public:
    int minOperations(vector<int>& nums) {
        int n = nums.size(), i = 0, j = 2, ans = 0;
        while(j < n){
            if(nums[i] == 0){
                ans++;
                for(int k = i; k < i + 3; k++){
                    nums[k] = nums[k] == 0 ? 1 : 0;
                }
            }
            i++, j++;
        }
        for(int i = 0; i < n; i++){
            if(nums[i] == 0) return -1;
        }
        return ans;
    }
};


```

</details>

<details>
<summary>Java</summary>

```java
// Java code
import java.util.List;

public class Solution {
    public int minOperations(List<Integer> nums) {
        int n = nums.size(), i = 0, j = 2, ans = 0;
        while (j < n) {
            if (nums.get(i) == 0) {
                ans++;
                for (int k = i; k < i + 3; k++) {
                    nums.set(k, nums.get(k) == 0 ? 1 : 0);
                }
            }
            i++;
            j++;
        }
        for (i = 0; i < n; i++) {
            if (nums.get(i) == 0) {
                return -1;
            }
        }
        return ans;
    }
}





```

</details>

## Minimum operations to make Binary elements equal to ||

<details>
<summary>Python</summary>

```python
class Solution:
    def minOperations(self, nums):
        n = len(nums)
        i = 0
        flips = 0
        while i < n:
            # Apply the flip effect based on the number of flips so far
            if flips % 2 == 1:
                nums[i] = 1 - nums[i]
            if nums[i] == 0:
                flips += 1
            i += 1
        return flips

```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <vector>

class Solution {
public:
    int minOperations(std::vector<int>& nums) {
        int n = nums.size();
        int i = 0;
        int flips = 0;
        
        // Traverse the entire array
        while (i < n) {
            // Apply the flip effect if the number of flips so far is odd
            if (flips % 2 == 1) {
                nums[i] = !nums[i];
            }
            // If the current element is 0, increment the flips counter
            if (nums[i] == 0) {
                flips++;
            }
            // Move to the next element
            i++;
        }
        // Return the total number of flips performed
        return flips;
   



```

</details>

<details>
<summary>Java</summary>

```java
import java.util.List;

public class Solution {
    public int minOperations(List<Integer> nums) {
        int n = nums.size();
        int i = 0;
        int flips = 0;
        while (i < n) {
            // Apply the flip effect based on the number of flips so far
            if (flips % 2 == 1) {
                nums.set(i, nums.get(i) == 0 ? 1 : 0);
            }
            if (nums.get(i) == 0) {
                flips++;
            }
            i++;
        }
        return flips;
    }
}


```

</details>

## Count the Number of Inversions

<details>
<summary>Python</summary>

```python
class Solution:
    def __init__(self):
        self.mod = int(1e9 + 7)
        self.dp = [[-1 for _ in range(401)] for _ in range(300)]
    
    def solve(self, i, n, m, cnt):
        if i == n:
            return 1
        if cnt > 400:
            return 0
        if self.dp[i][cnt] != -1:
            return self.dp[i][cnt]
        
        sum = 0
        for j in range(cnt, cnt + i + 1):
            if i in m and j != m[i]:
                continue
            sum = (sum + self.solve(i + 1, n, m, j)) % self.mod
        
        self.dp[i][cnt] = sum
        return sum
    
    def numberOfPermutations(self, n, requirements):
        m = {req[0]: req[1] for req in requirements}
        if 0 in m and m[0] != 0:
            return 0
        
        return self.solve(1, n, m, 0)


```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <vector>
#include <map>
#include <cstring>

class Solution {
public:
    int dp[300][401];
    int mod = 1e9 + 7;

    // Helper function to solve the problem using recursion and memoization
    int solve(int i, int n, std::map<int, int>& m, int cnt) {
        if (i == n)
            return 1; // Base case: reached the end
        if (cnt > 400)
            return 0; // Constraint: count exceeded 400
        if (dp[i][cnt] != -1)
            return dp[i][cnt]; // Return cached result if already computed

        int sum = 0;
        // Iterate over the range to calculate the sum
        for (int j = cnt; j <= cnt + i; j++) {
            if (m.find(i) != m.end() && j != m[i])
                continue; // Skip if there's a requirement and it doesn't match
            sum = (sum + solve(i + 1, n, m, j)) % mod; // Recursive call
        }
        return dp[i][cnt] = sum; // Cache the result and return it
    }

    // Function to compute the number of permutations
    int numberOfPermutations(int n, std::vector<std::vector<int>>& requirements) {
        std::map<int, int> m;
        memset(dp, -1, sizeof(dp)); // Initialize dp array with -1
        for (auto& req : requirements) {
            m[req[0]] = req[1]; // Populate the requirements map
        }

        if (m.find(0) != m.end() && m[0] != 0)
            return 0; // Return 0 if the first element has a conflicting requirement

        return solve(1, n, m, 0); // Start the recursion from the first element
    }
};

```

</details>

<details>
<summary>Java</summary>

```java
import java.util.HashMap;
import java.util.Map;

public class Solution {
    private static final int MOD = 1_000_000_007;
    private int[][] dp = new int[300][401];

    public Solution() {
        for (int i = 0; i < 300; i++) {
            for (int j = 0; j < 401; j++) {
                dp[i][j] = -1;
            }
        }
    }

    private int solve(int i, int n, Map<Integer, Integer> m, int cnt) {
        if (i == n) return 1;
        if (cnt > 400) return 0;
        if (dp[i][cnt] != -1) return dp[i][cnt];

        int sum = 0;
        for (int j = cnt; j <= cnt + i; j++) {
            if (m.containsKey(i) && j != m.get(i)) continue;
            sum = (sum + solve(i + 1, n, m, j)) % MOD;
        }
        dp[i][cnt] = sum;
        return sum;
    }

    public int numberOfPermutations(int n, List<int[]> requirements) {
        Map<Integer, Integer> m = new HashMap<>();
        for (int[] req : requirements) {
            m.put(req[0], req[1]);
        }

        if (m.containsKey(0) && m.get(0) != 0) return 0;

        return solve(1, n, m, 0);
    }
}

```

</details>

