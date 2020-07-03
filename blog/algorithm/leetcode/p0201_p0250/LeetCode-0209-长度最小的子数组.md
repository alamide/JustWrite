# 0209 长度最小的子数组
给定一个含有 n 个正整数的数组和一个正整数 s ，找出该数组中满足其和 ≥ s 的长度最小的连续子数组，并返回其长度。如果不存在符合条件的连续子数组，返回 0。

**示例：**
>输入: s = 7, nums = [2,3,1,2,4,3]  
 输出: 2  
 解释: 子数组 [4,3] 是该条件下的长度最小的连续子数组。  
 
**进阶：**
如果你已经完成了O(n) 时间复杂度的解法, 请尝试 O(n log n) 时间复杂度的解法。

一共有三种解法，我自己的解法是双指针  


### 最优解法，双指针，时间复杂度 O(n)，空间复杂度 O(1)

```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int res = Integer.MAX_VALUE;
        int sum = 0;
        int left = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];

            while (sum >= s) {
                int t = i - left + 1;
                if (t < res) {
                    res = i - left + 1;
                }
                sum -= nums[left];
                left++;
            }
        }

        return res == Integer.MAX_VALUE ? 0 : res;
    }
}

```


### 暴力求解法 时间复杂度 O(n^2)，空间复杂度 O(1)
```java
class Solution2 {
    public int minSubArrayLen(int s, int[] nums) {
        int res = Integer.MAX_VALUE;
        int sum;

        for (int i = 0; i < nums.length; i++) {
            sum = 0;
            for (int j = i; j < nums.length; j++) {
                sum += nums[j];
                if (sum >= s) {
                    res = Math.min(res, j - i + 1);
                    break;
                }
            }
        }

        return res == Integer.MAX_VALUE ? 0 : res;
    }
}
```
### 前缀和 + 二分查找

