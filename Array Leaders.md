
## Array Leaders

You are given an array  **`arr`**  of positive integers. Your task is to find all the leaders in the array. An element is considered a leader if it is greater than or equal to all elements to its right. The rightmost element is always a leader.

**Examples:**

**Input:** arr = [16, 17, 4, 3, 5, 2]
**Output:** [17, 5, 2] 
**Explanation:** Note that there is nothing greater on the right side of 17, 5 and, 2. 

**Input:** arr = [10, 4, 2, 4, 1]
**Output:** [10, 4, 4, 1]  
**Explanation:** Note that both of the 4s are in output, as to be a leader an equal element is also allowed on the right. side

**Input:** arr = [5, 10, 20, 40]  
**Output:** [40]  
**Explanation:** When an array is sorted in increasing order, only the rightmost element is leader.

**Input:** arr = [30, 10, 10, 5]  
**Output:** [30, 10, 10, 5]  
**Explanation:** When an array is sorted in non-increasing order, all elements are leaders.

**Constraints:**  
1 <= arr.size() <= 106  
0 <= arr[i] <= 106

**Expected Complexities**

Time Complexity: O(n)
Auxiliary Space: O(1)

---
## 🔥 Method 1: Naive Approach (Brute Force)

### 💡 Idea:
For each element `arr[i]`, check all elements to its **right**.  
If no element is greater than `arr[i]`, then it's a leader.

### 📝 Steps:
1.  Loop `i` from `0` to `n-1`.
2.  For each `arr[i]`, check `arr[j]` for `j = i+1...n-1`.
3.  If no `arr[j] > arr[i]`, mark `arr[i]` as leader. 
4.  Print/store leaders.
    

### 🔢 Complexity:
-   **Time:** O(n²) (Nested loop)
-   **Space:** O(1)
    

----------

### 🔹 Pseudocode
```
leaders = empty list
for i in 0 to n-1:
    leader = true
    for j in i+1 to n-1:
        if arr[j] > arr[i]:
            leader = false
            break
    if leader:
        leaders.append(arr[i])
return leaders
```

----------

### 🔹 C++ Code
```cpp
vector<int> arrayLeadersNaive(vector<int> &arr) 
{
    int n = arr.size();
    vector<int> leaders;
    for (int i = 0; i < n; i++) 
    {
        bool leader = true;
        for (int j = i + 1; j < n; j++) 
        {
            if (arr[j] > arr[i]) 
            {
                leader = false;
                break;
            }
        }
        if (leader) leaders.push_back(arr[i]);
    }
    return leaders;
}

```
----------

## 🔥 Method 2: Optimized Approach (Right-to-Left Scan)

### 💡 Idea:
Instead of checking all elements on the right every time,
-   Start from **rightmost element** (always leader).
-   Keep track of the **maximum element** seen so far.
-   If `arr[i] >= maxRight`, it's a leader.
    

### 📝 Steps:
1.  Initialize `maxRight = -∞`.
2.  Loop from `i = n-1` to `0`.
3.  If `arr[i] >= maxRight`, mark it as leader & update `maxRight`.
4.  Reverse the result (since we collected from right to left).
    

### 🔢 Complexity:
-   **Time:** O(n)
-   **Space:** O(1) (excluding result storage)
----------

### 🔹 Pseudocode
```
leaders = empty list
maxRight = -∞
for i from n-1 downto 0:
    if arr[i] >= maxRight:
        leaders.append(arr[i])
        maxRight = arr[i]
reverse leaders
return leaders

```
----------

### 🔹 C++ Code
```cpp
vector<int> arrayLeadersOptimized(vector<int> &arr) 
{
    int n = arr.size();
    vector<int> leaders;
    int maxRight = INT_MIN;

    for (int i = n - 1; i >= 0; i--) 
    {
        if (arr[i] >= maxRight) 
        {
            leaders.push_back(arr[i]);
            maxRight = arr[i];
        }
    }
    reverse(leaders.begin(), leaders.end());
    return leaders;
}

```
----------

## 🔥 Method 3: Optimized In-Place Printing (O(1) Extra Space)

### 💡 Idea:
We can directly print leaders while scanning from right to left without storing all in a separate vector.  
This avoids extra space for storing results.

### 📝 Steps:
1.  Initialize `maxRight = -∞`.
2.  Traverse array from right to left.
3.  If `arr[i] >= maxRight`, print it and update `maxRight`.
4.  Reverse the order of printing if needed.
    

----------

### 🔢 Complexity:
-   **Time:** O(n)
-   **Space:** O(1)
----------

### 🔹 Pseudocode
```
maxRight = -∞
for i from n-1 downto 0:
    if arr[i] >= maxRight:
        print(arr[i])
        maxRight = arr[i]
```
----------

### 🔹 C++ Code
```cpp
void printArrayLeadersInPlace(vector<int> &arr) 
{
    int n = arr.size();
    int maxRight = INT_MIN;

    for (int i = n - 1; i >= 0; i--) 
    {
        if (arr[i] >= maxRight) 
        {
            cout << arr[i] << " ";
            maxRight = arr[i];
        }
    }
    cout << endl; // Order is reversed; can be fixed if needed.
}
```
----------

✅ **Best Choice:** Use **Right-to-Left Scan (Method 2)** for efficiency and clarity.
