## Find if Digit Game Can Be Won

<details>
<summary>Python</summary>

```python
# Python code
class Solution:
    def canAliceWin(self, nums: List[int]) -> bool:
        singleSum = 0
        doubleSum = 0
        for num in nums:
            if num < 10:
                singleSum += num
            else:
                doubleSum += num
        return singleSum > doubleSum or doubleSum > singleSum


```

</details>

<details>
<summary>Cpp</summary>

```cpp
 class Solution {
public:
    bool canAliceWin(std::vector<int>& nums) {
        int singleSum = 0, doubleSum = 0;
        for (int num : nums) {
            if (num < 10) {
                singleSum += num;
            } else {
                doubleSum += num;
            }
        }
        return singleSum > doubleSum || doubleSum > singleSum;
    }
};


```

</details>

<details>
<summary>Java</summary>

```java
class Solution {
    public boolean canAliceWin(int[] nums) {
        int singleSum = 0, doubleSum = 0;
        for (int num : nums) {
            if (num < 10) {
                singleSum += num;
            } else {
                doubleSum += num;
            }
        }
        return singleSum > doubleSum || doubleSum > singleSum;
    }
}



```

</details>

## Find the Count of Numbers Which Are Not Special

<details>
<summary>Python</summary>

```python
class Solution:
    def nonSpecialCount(self, l: int, r: int) -> int:
        # Calculate the limit up to which we need to find prime numbers
        lim = int(math.sqrt(r))
        
        # Create a list to mark primes up to lim using Sieve of Eratosthenes
        is_prime = [True] * (lim + 1)
        is_prime[0] = is_prime[1] = False # 0 and 1 are not prime numbers

        # Sieve of Eratosthenes to mark non-prime numbers
        for i in range(2, int(math.sqrt(lim)) + 1):
            if is_prime[i]:
                for j in range(i * i, lim + 1, i):
                    is_prime[j] = False

        # Count special numbers in the range [l, r]
        special_count = 0
        for i in range(2, lim + 1):
            if is_prime[i]:
                square = i * i
                if l <= square <= r:
                    special_count += 1

        # Total numbers in the range [l, r]
        total_count = r - l + 1

        # Calculate non-special numbers
        return total_count - special_count



```

</details>

<details>
<summary>Cpp</summary>

```cpp

class Solution {
public:
    int nonSpecialCount(int l, int r) {
        // Calculate the limit up to which we need to find prime numbers
        int lim = (int)(sqrt(r));

        // Create a boolean array to mark primes up to lim using Sieve of Eratosthenes
        vector<bool> v(lim + 1, true);
        v[0] = v[1] = false; // 0 and 1 are not prime numbers

        // Sieve of Eratosthenes to mark non-prime numbers
        for (int i = 2; i * i <= lim; i++) {
            if (v[i]) {
                for (int j = i * i; j <= lim; j += i) {
                    v[j] = false;
                }
            }
        }

        // Count special numbers in the range [l, r]
        int cnt = 0;
        for (int i = 2; i <= lim; i++) {
            if (v[i]) {
                int square = i * i;
                if (square >= l && square <= r) {
                    cnt++;
                }
            }
        }

        // Total numbers in the range [l, r]
        int totalCount = r - l + 1;

        // Calculate non-special numbers
        return totalCount - cnt;
    }
};


```

</details>

<details>
<summary>Java</summary>

```java
class Solution {
    public int nonSpecialCount(int l, int r) {
        // Calculate the limit up to which we need to find prime numbers
        int lim = (int) Math.sqrt(r);
        
        // Create an array to mark primes up to lim using Sieve of Eratosthenes
        boolean[] isPrime = new boolean[lim + 1];
        Arrays.fill(isPrime, true);
        isPrime[0] = isPrime[1] = false; // 0 and 1 are not prime numbers

        // Sieve of Eratosthenes to mark non-prime numbers
        for (int i = 2; i * i <= lim; i++) {
            if (isPrime[i]) {
                for (int j = i * i; j <= lim; j += i) {
                    isPrime[j] = false;
                }
            }
        }

        // Count special numbers in the range [l, r]
        int specialCount = 0;
        for (int i = 2; i <= lim; i++) {
            if (isPrime[i]) {
                int square = i * i;
                if (square >= l && square <= r) {
                    specialCount++;
                }
            }
        }

        // Total numbers in the range [l, r]
        int totalCount = r - l + 1;

        // Calculate non-special numbers
        return totalCount - specialCount;
    }
}





```

</details>

## Count the Number of Substrings With Dominant Ones

<details>
<summary>Python</summary>

```python
class Solution:
    def numberOfSubstrings(self, s: str) -> int:
        n = len(s)
        result = 0
        
        # Iterate through possible zero counts (1 to sqrt(n))
        for k in range(1, int(n**0.5) + 1):
            zeros = deque()  # Queue to store positions of zeros
            lastzero = -1    # Position of the zero before the first zero in our window
            ones = 0         # Count of ones in our current window
            
            # Scan through the string
            for right in range(n):
                if s[right] == '0':
                    zeros.append(right)
                    # If we have more than k zeros, remove the leftmost one
                    while len(zeros) > k:
                        ones -= (zeros[0] - lastzero - 1)  # Subtract ones between lastzero and the removed zero
                        lastzero = zeros.popleft()
                else:
                    ones += 1
                
                # If we have exactly k zeros and at least k^2 ones
                if len(zeros) == k and ones >= k**2:
                    # Add the minimum of:
                    # 1. Number of ways to extend to the left (zeros[0] - lastzero)
                    # 2. Number of ways to extend to the right (ones - k**2 + 1)
                    result += min(zeros[0] - lastzero, ones - k**2 + 1)
        
        # Handle all-ones substrings
        i = 0
        while i < n:
            if s[i] == '0':
                i += 1
                continue
            sz = 0
            while i < n and s[i] == '1':
                sz += 1
                i += 1
            # Add number of all-ones substrings
            result += (sz * (sz + 1)) // 2
        
        return result


```

</details>

<details>
<summary>Cpp</summary>

```cpp
class Solution {
public:
    int numberOfSubstrings(string s) {
        int n = s.length();
        int cnt = 0;
        
        vector<int> zro;
        for (int i = 0; i < n; i ++)
            if (s[i] == '0') zro.push_back(i);
        
        if (zro.empty()) return n*(n+1)/2;
        int zro_ind = 0;
        
        for (int l = 0; l < n; l ++) {
            while (zro_ind < zro.size() && zro[zro_ind] < l) zro_ind ++;
            
            vector<int> valid_zro;
            for (int z = zro_ind; z < zro.size() && z < (zro_ind+201); z ++)
                valid_zro.push_back(zro[z]);
            valid_zro.push_back(n);
            
            int zro_cnt = 0;
            int last = l;
            
            for (auto ind : valid_zro) {
                int min_one = zro_cnt*zro_cnt;
                int min_ind = max(l + min_one + zro_cnt - 1, last);

                if (min_ind < ind) cnt += (ind - min_ind); 
                
                last = ind;
                zro_cnt ++;
            }
        }
        return cnt;
    }
};


```

</details>

<details>
<summary>Java</summary>

```java

class Solution {
    public int numberOfSubstrings(String s) {
        int output = 0;
        int prefix[] = new int[s.length()];
        for(int i=0;i<s.length();i++){
            if(i == 0) prefix[i] = (s.charAt(i) == '1')? 1:0;
            else prefix[i] = prefix[i-1] + ((s.charAt(i) == '1')? 1:0);
        }
        for(int i=0;i<s.length();i++){
            int count = 0,one = 0;
            for(int j=i;j<s.length();j++){
                one = prefix[j]-((i == 0)?0:prefix[i-1]); //count of one
                count = j-i+1-one;  //count of zero
                if(count*count > one)  j+=((count*count)-one-1);  //jump where next soltuion is possible
                if(count*count <= one) {
                    int kl = (int)Math.sqrt(one);
                    output++;
                    if(kl>count){  //again jump where zero can be greater than one.
                        output += (j+(kl-count))>=s.length()?(s.length()-j-1):(kl-count); //condition added just to ensure not to exceed the s.length()
                        j = j+(kl-count);
                    }
                }
            }
        }
        return output;
    }
}


```

</details>

##  Check if the Rectangle Corner Is Reachable

<details>
<summary>Python</summary>

```python

class Solution:
    def canReachCorner(self, X: int, Y: int, A: List[List[int]]) -> bool:
        def find(i):
            if f[i] != i:
                f[i] = find(f[i])
            return f[i]

        n = len(A)
        f = list(range(n + 2))
        for i in range(n):
            x, y, r = A[i]
            if x - r <= 0 or y + r >= Y:
                f[find(n)] = find(i)
            if x + r >= X or y - r <= 0:
                f[find(n + 1)] = find(i)
            for j in range(i):
                x2, y2, r2 = A[j]
                if (x - x2) ** 2 + (y - y2) ** 2 <= (r + r2) ** 2:
                    f[find(i)] = find(j)
        return find(n) != find(n + 1)
```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <vector>
using namespace std;

class Solution {
public:
    bool canReachCorner(int X, int Y, vector<vector<int>>& A) {
        int n = A.size();
        vector<int> f(n + 2);
        for (int i = 0; i < n + 2; i++) {
            f[i] = i;
        }

        for (int i = 0; i < n; i++) {
            int x = A[i][0];
            int y = A[i][1];
            int r = A[i][2];

            if (x - r <= 0 || y + r >= Y) {
                f[find(f, n)] = find(f, i);
            }
            if (x + r >= X || y - r <= 0) {
                f[find(f, n + 1)] = find(f, i);
            }

            for (int j = 0; j < i; j++) {
                int x2 = A[j][0];
                int y2 = A[j][1];
                int r2 = A[j][2];

                if ((x - x2) * (x - x2) + (y - y2) * (y - y2) <= (r + r2) * (r + r2)) {
                    f[find(f, i)] = find(f, j);
                }
            }
        }

        return find(f, n) != find(f, n + 1);
    }

private:
    int find(vector<int>& f, int i) {
        if (f[i] != i) {
            f[i] = find(f, f[i]);
        }
        return f[i];
    }
};

```

</details>

<details>
<summary>Java</summary>

```java
class Solution {
    public boolean canReachCorner(int X, int Y, int[][] A) {
        int n = A.length;
        int[] f = new int[n + 2];
        
        for (int i = 0; i < n + 2; i++) {
            f[i] = i;
        }

        for (int i = 0; i < n; i++) {
            int x = A[i][0];
            int y = A[i][1];
            int r = A[i][2];

            if (x - r <= 0 || y + r >= Y) {
                f[find(f, n)] = find(f, i);
            }

            if (x + r >= X || y - r <= 0) {
                f[find(f, n + 1)] = find(f, i);
            }

            for (int j = 0; j < i; j++) {
                int x2 = A[j][0];
                int y2 = A[j][1];
                int r2 = A[j][2];

                if ((x - x2) * (x - x2) + (y - y2) * (y - y2) <= (r + r2) * (r + r2)) {
                    f[find(f, i)] = find(f, j);
                }
            }
        }

        return find(f, n) != find(f, n + 1);
    }

    private int find(int[] f, int i) {
        if (f[i] != i) {
            f[i] = find(f, f[i]);
        }
        return f[i];
    }
}


```

</details>


