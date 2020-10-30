# LeetCode 27: Remove Element

Given an array *nums* and a value *val*, remove all instances of that value [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array in-place** with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example 1:**

```
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.
It doesn't matter what you leave beyond the returned length.
```

**Example 2:**

```
Given nums = [0,1,2,2,3,0,4,2], val = 2,

Your function should return length = 5, with the first five elements of nums containing 0, 1, 3, 0, and 4.
Note that the order of those five elements can be arbitrary.
It doesn't matter what values are set beyond the returned length.
```

**Clarification:**

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by **reference**, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

```
// nums is passed in by reference. (i.e., without making a copy)
int len = removeElement(nums, val);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```

## Java

```java
package com.blessed.leetcode.easy;

public class LeetCode27 {
    /**
     * input:  1 2 2 3 1 1 3 4 , key = 3
     * output: 1 2 2 1 1 4
     * @param nums
     * @param val
     * @return
     */
    public int removeElement(int[] nums, int val) {
        if (nums.length == 0) return 0;
        int i = 0, j = 0;
        while (j < nums.length) {
            if (nums[i] != nums[j]) {
                int temp = nums[i];
                nums[i] = nums[j];
                nums[j] = temp;
            }

            if (j <= i || nums[j] == val) {
                j++;
            }
            if (nums[i] != val) {
                i++;
            }
        }
        return i;
    }

    public static void main(String[] args) {
        int[] nums = new int[]{1, 2, 2, 3, 1, 1, 3, 4};
        int key = 3;
        System.out.println(new LeetCode27().removeElement(nums, key));
    }
}

```

## Python

```python
class Solution:
    def removeElement(self, nums, val):
        if len(nums) == 0:
            return 0
        i, j = 0, 0
        while j < len(nums):
            if nums[i] != nums[j]:
                nums[i], nums[j] = nums[j], nums[i]
            if j <= i or nums[j] == val:
                j = j + 1
            if nums[i] != val:
                i = i + 1
        return i


if __name__ == '__main__':
    nums = [1, 2, 2, 3, 1, 1, 3, 4]
    key = 3
    print(Solution().removeElement(nums, key))
```

## 分析

![](../img/Leetcode27.png)
