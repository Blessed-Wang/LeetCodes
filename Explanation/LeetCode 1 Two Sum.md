# LeetCode 1 Two Sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## Java

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            map.put(nums[i], i);
        }
        for (int i = 0; i < nums.length; i++) {
            int k = target - nums[i];
            Integer otherIndex = map.get(k);
            if (otherIndex != null && !otherIndex.equals(i)) {
                result[0] = i;
                result[1] = otherIndex;
            }
        }
        return result;
    }
}
```

## Python

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dic = {}
        res = []
        for index, value in enumerate(nums):
            dic[value] = index
        for index, value in enumerate(nums):
            k = target - value
            other_index = index
            if k in dic.keys():
                other_index = dic[k]
            else:
                continue
            if other_index is not index:
                res.append(index)
                res.append(other_index)
                break
        return res
```

## 分析

题目大意：给一个数组，和一个目标数字，问这里面哪两个数加起来等于这个目标数字，返回它们的下标。暴力破解可以，但是不可取。这里我们使用Hash算法，键是第$i$个元素的值（$i=0,1,2,\cdots$），值就是$i$，存储后，我们去遍历这个数组，在访问第$i$个元素后，我们去Hash表中查找是否存在$target-nums_i$的键，如果存在就说明我们找到了这两个数字，根据键查出其索引值只需要$O(1)$的时间。