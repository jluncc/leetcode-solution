532. #### [数组中的K-diff数对](https://leetcode-cn.com/problems/k-diff-pairs-in-an-array/submissions/)

给定一个整数数组和一个整数 k, 你需要在数组里找到不同的 k-diff 数对。这里将 k-diff 数对定义为一个整数对 (i, j), 其中 i 和 j 都是数组中的数字，且两数之差的绝对值是 k.

**示例 1:**

```
输入: [3, 1, 4, 1, 5], k = 2
输出: 2
解释: 数组中有两个 2-diff 数对, (1, 3) 和 (3, 5)。
尽管数组中有两个1，但我们只应返回不同的数对的数量。
```

**示例 2:**

```
输入:[1, 2, 3, 4, 5], k = 1
输出: 4
解释: 数组中有四个 1-diff 数对, (1, 2), (2, 3), (3, 4) 和 (4, 5)。
```

**示例 3:**

```
输入: [1, 3, 1, 5, 4], k = 0
输出: 1
解释: 数组中只有一个 0-diff 数对，(1, 1)。
```

**注意:**

```
数对 (i, j) 和数对 (j, i) 被算作同一数对。
数组的长度不超过10,000。
所有输入的整数的范围在 [-1e7, 1e7]。
```

------

**参考代码**

Java 实现

```java
class Solution {
    public int findPairs(int[] nums, int k) {
        Arrays.sort(nums);
        int result = 0;
        boolean notEqualBefore = true;
        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] == nums[i -1]) continue;

            for (int j = i + 1; j < nums.length; j++) {
                if (k == 0) {
                    if (nums[j] == nums[i]) {
                        if (notEqualBefore) {
                            result++;
                            notEqualBefore = false;
                        }
                    } else {
                        notEqualBefore = true;
                    }
                } else {
                    if (nums[j] == nums[j - 1]) continue;
                    if (nums[j] - nums[i] > k) break;
                    if (nums[j] - nums[i] == k) result++;
                }
            }
        }
        return result;
    }
}
```