
# 🚀 Minimum Distance Between Three Equal Elements I_ 🧠

The problem can be found at the following link: [LeetCode Problem](https://leetcode.com/problems/minimum-distance-between-three-equal-elements-i/)

---

## 💡 **Problem Description:**

You are given an integer array `nums`.

A tuple `(i, j, k)` of **3 distinct indices** is **good** if `nums[i] == nums[j] == nums[k]`.

The **distance** of a good tuple is defined as:  
`abs(i - j) + abs(j - k) + abs(k - i)`,  
where `abs(x)` denotes the absolute value.

Return the **minimum possible distance** of any good tuple.  
If no such tuple exists, return `-1`.

---

### **Example 1:**

**Input:**
```text
nums = [1, 2, 1, 1, 3]
```

**Output:**
```text
6
```

**Explanation:**  
The good tuple `(0, 2, 3)` gives distance  
`|0 - 2| + |2 - 3| + |3 - 0| = 2 + 1 + 3 = 6`.

---

### **Example 2:**

**Input:**
```text
nums = [1, 1, 2, 3, 2, 1, 2]
```

**Output:**
```text
8
```

**Explanation:**  
The good tuple `(2, 4, 6)` gives  
`|2 - 4| + |4 - 6| + |6 - 2| = 2 + 2 + 4 = 8`.

---

### **Example 3:**

**Input:**
```text
nums = [1]
```

**Output:**
```text
-1
```

**Explanation:**  
No number appears three times, so there is no good tuple.

---

### **Constraints:**
- (1 ≤ nums.length ≤ 100)
- (1 ≤ nums[i] ≤ n)

---

## 🎯 **My Approach:**

### **Brute Force Method (O(n³)):**

1. Use **three nested loops** to check all possible triplets `(i, j, k)`.
2. If all three elements are equal, compute the distance.
3. Track the minimum distance found.
4. Return `-1` if no triplet is found.

### **Optimized Approach (O(n)):**

1. Use a **HashMap** to store the **indices** of each number.
2. For each number that appears at least 3 times:
   - Sort its index list.
   - For every **3 consecutive indices**, compute  
     `distance = 2 × (last - first)`.
   - Keep track of the smallest distance.
3. Return the minimum or `-1` if no such number exists.

---

## 🧮 **Example Dry Run**

### Input:
```
nums = [1, 2, 1, 1, 3]
```

### Step 1: Build map
```
1 → [0, 2, 3]
2 → [1]
3 → [4]
```

### Step 2: Process number `1`
Triplet (0, 2, 3):
```
distance = 2 × (3 - 0) = 6
```

✅ Minimum distance = 6  
No other numbers have 3 or more occurrences.

### Output:
```
6
```

---

## 🕒 **Time and Space Complexity** 📝

| Approach | Time Complexity | Space Complexity | Explanation |
|-----------|------------------|------------------|-------------|
| **Brute Force** | O(n³) | O(1) | Checks all possible triplets |
| **Optimized (HashMap + Math Trick)** | O(n) | O(n) | Groups indices and checks only consecutive triplets |

---

## 🧑‍💻 **Code (Java)**

### **Brute Force Approach**

```java
class Solution {
    public int minimumDistance(int[] nums) {
        int n = nums.length;
        int minDistance = Integer.MAX_VALUE;

        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                for (int k = j + 1; k < n; k++) {
                    if (nums[i] == nums[j] && nums[j] == nums[k]) {
                        int distance = Math.abs(i - j) + Math.abs(j - k) + Math.abs(k - i);
                        minDistance = Math.min(minDistance, distance);
                    }
                }
            }
        }

        return minDistance == Integer.MAX_VALUE ? -1 : minDistance;
    }
}
```

---

### **Optimized Approach (HashMap + Formula Trick)**

```java
import java.util.*;

class Solution {
    public int minimumDistance(int[] nums) {
        int n = nums.length;
        Map<Integer, List<Integer>> map = new HashMap<>();

        // Step 1: Store indices for each number
        for (int i = 0; i < n; i++) {
            map.computeIfAbsent(nums[i], k -> new ArrayList<>()).add(i);
        }

        int minDistance = Integer.MAX_VALUE;

        // Step 2: Check each number’s list
        for (List<Integer> indices : map.values()) {
            if (indices.size() < 3) continue;

            // Step 3: Only check consecutive triplets
            for (int i = 0; i < indices.size() - 2; i++) {
                int first = indices.get(i);
                int third = indices.get(i + 2);
                int distance = 2 * (third - first);
                minDistance = Math.min(minDistance, distance);
            }
        }

        return minDistance == Integer.MAX_VALUE ? -1 : minDistance;
    }
}
```

---

## 💬 **Explanation Summary**

- The brute force solution checks **every possible triplet**, hence O(n³).
- The optimized one uses a **math simplification**:
  - For any sorted triple (i, j, k):  
    `|i - j| + |j - k| + |k - i| = 2 × (k - i)`
- So, only the **first and last indices** matter in each triple,  
  making it run efficiently in linear time.

---

## ✅ **Sample Outputs**

| Input | Output | Explanation |
|--------|---------|-------------|
| `[1, 2, 1, 1, 3]` | 6 | (0, 2, 3) gives 6 |
| `[1, 1, 2, 3, 2, 1, 2]` | 8 | (2, 4, 6) gives 8 |
| `[1]` | -1 | No triplet found |

---

## 🏁 **Final Thoughts**

This problem teaches:
- How to **identify repeated values** using a map.
- How to simplify formulas for better performance.
- How **mathematical reasoning** can turn O(n³) → O(n).

---

<div align="center">
  <h3><b>📍Visitor Count</b></h3>
</div>

<p align="center">
  <img src="https://visitor-badge.laobi.icu/badge?page_id=EswarIsukapalli.LeetCode-Minimum-Distance-Between-Three-Equal-Elements" />
</p>
