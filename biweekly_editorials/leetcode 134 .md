## Alternating groups |

<details>
<summary>Python</summary>

```python
# Python code
class Solution:
    def numberOfAlternatingGroups(self, colors: List[int]) -> int:
        n = len(colors)
        colors += colors[:]  # Append a copy of colors to itself
        
        ans = 0
        for i in range(n):
            if colors[i] == colors[i + 2] and colors[i] != colors[i + 1]:
                ans += 1
        return ans


```

</details>

<details>
<summary>Cpp</summary>

```cpp
 #include <vector>
using namespace std;

class Solution {
public:
    int numberOfAlternatingGroups(vector<int>& colors) {
        int n = colors.size();
        colors.insert(colors.end(), colors.begin(), colors.end());  // Append a copy of colors to itself
        
        int ans = 0;
        for (int i = 0; i < n; i++) {
            if (colors[i] == colors[i + 2] && colors[i] != colors[i + 1]) {
                ans++;
            }
        }
        return ans;
    }
};



```

</details>

<details>
<summary>Java</summary>

```java
class Solution {
    public int numberOfAlternatingGroups(int[] colors) {
        int n = colors.length;
        int[] extendedColors = new int[2 * n];
        for (int i = 0; i < n; i++) {
            extendedColors[i] = colors[i];
            extendedColors[i + n] = colors[i];
        }
        
        int ans = 0;
        for (int i = 0; i < n; i++) {
            if (extendedColors[i] == extendedColors[i + 2] && extendedColors[i] != extendedColors[i + 1]) {
                ans++;
            }
        }
        return ans;
    }
}

```

</details>

## maximum points after enemy bottles

<details>
<summary>Python</summary>

```python
class Solution:
    def maximumPoints(self, enemyEnergies: List[int], currentEnergy: int) -> int:
        profit = 0
        n = len(enemyEnergies)
        enemyEnergies.sort()
        
        if enemyEnergies[0] > currentEnergy:
            return 0
        
        j = n - 1
        while j >= 0:
            if enemyEnergies[0] <= currentEnergy:
                profit += currentEnergy // enemyEnergies[0]
                currentEnergy %= enemyEnergies[0]
            else:
                currentEnergy += enemyEnergies[j]
                j -= 1
        
        return profit



```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    long long maximumPoints(vector<int>& enemyEnergies, int currentEnergy) {
        long long profit = 0;
        int n = enemyEnergies.size();
        sort(enemyEnergies.begin(), enemyEnergies.end());
        
        if (enemyEnergies[0] > currentEnergy)
            return 0;
        
        int j = n - 1;
        while (j >= 0) {
            if (enemyEnergies[0] <= currentEnergy) {
                profit += currentEnergy / enemyEnergies[0];
                currentEnergy %= enemyEnergies[0];
            } else {
                currentEnergy += enemyEnergies[j];
                j--;
            }
        }
        
        return profit;
    }
};


```

</details>

<details>
<summary>Java</summary>

```java
// Java code
import java.util.Arrays;

class Solution {
    public long maximumPoints(int[] enemyEnergies, int currentEnergy) {
        long profit = 0;
        int n = enemyEnergies.length;
        Arrays.sort(enemyEnergies);
        
        if (enemyEnergies[0] > currentEnergy)
            return 0;
        
        int j = n - 1;
        while (j >= 0) {
            if (enemyEnergies[0] <= currentEnergy) {
                profit += currentEnergy / enemyEnergies[0];
                currentEnergy %= enemyEnergies[0];
            } else {
                currentEnergy += enemyEnergies[j];
                j--;
            }
        }
        
        return profit;
    }
}






```

</details>

## Alternating groups ||

<details>
<summary>Python</summary>

```python
def numberOfAlternatingGroups(colors, k):
    last = colors[0]
    ans = 0
    count = 1
    
    for i in range(1, len(colors)):
        count = count + 1 if colors[i] != last else 1
        if count >= k:
            ans += 1
        last = colors[i]
    
    for i in range(k - 1):  # Circulate one more time up to k-1
        count = count + 1 if colors[i] != last else 1
        if count >= k:
            ans += 1
        last = colors[i]
    
    return ans



```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <vector>
using namespace std;

int numberOfAlternatingGroups(vector<int>& colors, int k) {
    int last = colors[0], ans = 0, count = 1; 
    for(int i = 1; i < colors.size(); ++i){
        count = (colors[i] != last)? count + 1 : 1;
        if(count >= k) ans++;
        last = colors[i];
    }
    for(int i = 0; i < k - 1; ++i) { // Circulate one more time up to k-1
        count = (colors[i] != last)? count + 1 : 1;
        if(count >= k) ans++;
        last = colors[i];
    }
    return ans;
}


```

</details>

<details>
<summary>Java</summary>

```java
import java.util.*;

class Solution {
    public int numberOfAlternatingGroups(List<Integer> colors, int k) {
        int last = colors.get(0), ans = 0, count = 1;
        for (int i = 1; i < colors.size(); ++i) {
            count = (colors.get(i) != last) ? count + 1 : 1;
            if (count >= k) ans++;
            last = colors.get(i);
        }
        for (int i = 0; i < k - 1; ++i) { // Circulate one more time up to k-1
            count = (colors.get(i) != last) ? count + 1 : 1;
            if (count >= k) ans++;
            last = colors.get(i);
        }
        return ans;
    }
}


```

</details>

## Number of subarrays with AND Value of K

<details>
<summary>Python</summary>

```python
class Solution:
    def countSubarrays(self, nums: List[int], k: int) -> int:
        return self.atLeastK(nums, k) - self.atLeastK(nums, k + 1)
    
    def atLeastK(self, nums: List[int], k: int) -> int:
        ans = 0
        temp = [0] * 32
        
        l = 0
        for r in range(len(nums)):
            # Update frequency of each bit in temp based on nums[r]
            for i in range(32):
                if nums[r] & (1 << i):  # Check if ith bit is set in nums[r]
                    temp[i] += 1
            
            # Adjust left pointer l to ensure the subarray [l, r] meets the criteria
            while (r - l + 1) > 0 and self.calc(temp, r - l + 1) < k:
                # Reduce counts in temp for nums[l] as it moves out of the window
                for i in range(32):
                    if nums[l] & (1 << i):  # Check if ith bit is set in nums[l]
                        temp[i] -= 1
                l += 1
            
            # Count all subarrays ending at r that satisfy the condition
            ans += (r - l + 1)
        
        return ans
    
    def calc(self, temp: List[int], w: int) -> int:
        ans = 0
        for i in range(32):
            if temp[i] == w:
                ans += (1 << i)  # Set ith bit in ans
        return ans

```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    long long countSubarrays(vector<int> &nums, int k) {
        return atLeastK(nums, k) - atLeastK(nums, k + 1);
    }

    long long atLeastK(vector<int>& nums, int k) {
        long long ans = 0;
        vector<int> temp(32, 0);

        int l = 0;
        for (int r = 0; r < nums.size(); r++) {
            // Update frequency of each bit in temp based on nums[r]
            for (int i = 0; i < 32; i++) {
                if ((1 << i) & nums[r]) { // Check if ith bit is set in nums[r]
                    temp[i]++;
                }
            }

            // Adjust left pointer l to ensure the subarray [l, r] meets the criteria
            while ((r - l + 1) > 0 && calc(temp, r - l + 1) < k) {
                // Reduce counts in temp for nums[l] as it moves out of the window
                for (int i = 0; i < 32; i++) {
                    if ((1 << i) & nums[l]) { // Check if ith bit is set in nums[l]
                        temp[i]--;
                    }
                }
                l++;
            }

            // Count all subarrays ending at r that satisfy the condition
            ans += (r - l + 1);
        }

        return ans;
    }

    // Function to calculate the AND from frequency vector
    int calc(vector<int>& temp, int w) {
        int ans = 0;
        for (int i = 0; i < 32; i++) {
            if (temp[i] == w) {
                ans += (1 << i); // Set ith bit in ans
            }
        }
        return ans;
    }
};

```

</details>

<details>
<summary>Java</summary>

```java
import java.util.*;

class Solution {
    public long countSubarrays(int[] nums, int k) {
        return atLeastK(nums, k) - atLeastK(nums, k + 1);
    }
    
    public long atLeastK(int[] nums, int k) {
        long ans = 0;
        int[] temp = new int[32]; // Temporary array to count occurrences of each bit position
        
        int l = 0;
        for (int r = 0; r < nums.length; r++) {
            // Update frequency of each bit in temp based on nums[r]
            for (int i = 0; i < 32; i++) {
                if ((1 << i & nums[r]) != 0) { // Check if ith bit is set in nums[r]
                    temp[i]++;
                }
            }
            
            // Adjust left pointer l to ensure the subarray [l, r] meets the criteria
            while ((r - l + 1) > 0 && calc(temp, r - l + 1) < k) {
                // Reduce counts in temp for nums[l] as it moves out of the window
                for (int i = 0; i < 32; i++) {
                    if ((1 << i & nums[l]) != 0) { // Check if ith bit is set in nums[l]
                        temp[i]--;
                    }
                }
                l++;
            }
            
            // Count all subarrays ending at r that satisfy the condition
            ans += (r - l + 1);
        }
        
        return ans;
    }
    
    // Function to calculate the AND from frequency array
    public int calc(int[] temp, int w) {
        int ans = 0;
        for (int i = 0; i < 32; i++) {
            if (temp[i] == w) {
                ans += (1 << i); // Set ith bit in ans
            }
        }
        return ans;
    }
}


```

</details>

