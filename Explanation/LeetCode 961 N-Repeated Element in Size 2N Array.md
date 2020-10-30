# LeetCode 961: N-Repeated Element in Size `2N` Array

In a array `A` of size `2N`, there are `N+1` unique elements, and exactly one of these elements is repeated N times.

Return the element repeated `N` times.



**Example 1:**

```
Input: [1,2,3,3]
Output: 3
```

**Example 2:**

```
Input: [2,1,2,5,3,2]
Output: 2
```

**Example 3:**

```
Input: [5,1,5,2,5,3,5,4]
Output: 5 
```

**Note:**

1. `4 <= A.length <= 10000`
2. `0 <= A[i] < 10000`
3. `A.length` is even

## Java

```java
package com.blessed.leetcode.easy;

public class LeetCode961 {
    public int repeatedNTimes(int[] A){
        if (A[A.length -1] == A[0] || A[A.length - 2] == A[0]) {
            return A[0];
        }
        if (A[0] == A[1] || A[A.length -1] == A[1]){
            return A[1];
        }

        for (int i = 2; i < A.length; i++) {
            if (A[i-1] == A[i] || A[i-2] == A[i]){
                return A[i];
            }
        }
        return 0;
    }

    public static void main(String[] args) {
        var solution = new LeetCode961();
        var res = solution.repeatedNTimes(new int[]{9, 5, 6, 9});
        System.out.println(res);
    }
}

```

## Python

```python
class Solution:
    def repeatedNTimes(self, A):
        """
        :param a: list[int]
        :return: int
        """
        for i in range(len(A)):
            if A[i - 1] == A[i] or A[i - 2] == A[i]:
                return A[i]


if __name__ == '__main__':
    solution = Solution()
    res = solution.repeatedNTimes(list([1, 2, 3, 3]))
    print(res)
    res = solution.repeatedNTimes(list([2, 1, 2, 5, 3, 2]))
    print(res)
    res = solution.repeatedNTimes(list([5, 1, 5, 2, 5, 3, 5, 4]))
    print(res)
```

## 分析

$2N$个数字，有$N$个数字是重复，就是要找到这重复$N$次的数字。

- **方法一**：可以排序：然后遍历，挨着两个相同的就是结果

- **方法二**：可以对每个数字出现的次数进行计数，使用字典（映射）数据结构进行记录，然后输出出现次数为$N$的数字，或者在计数的时候，只要当一个数字出现两次的时候就可以结束了

- **方法三**：看一遍这个数组，就应该知道答案了，我们只要找到两个相同的数字，这就是结果。那么一个有$2N$个数字的数组，$N$个是相同的，要想两个相同的隔得最远，就是将$N$个数字塞到$N-1$个不同的数字里，就是一个隔着一个放。

  - 如果前$N$个数字互不相同，那么第$N+1$个数字到第$2N$个数字可能相同，此时只要循环$N$次就可以知道有两个数字相同了，这也是最坏的情况。所以时间复杂度为$\mathcal{O}(N)$。
  - 在上面的情况中有一种情形，就是将第$N$个和第$N+1$个数字对换位置，那么此时我们不需要去循环到第$N+1$的位置，而是我们在第$N-1$个位置时候，不但和第$N$个进行了比较，还和第$N+1$个进行比较，此时也已经得出答案。

  所以算法就是，遍历整个数组，每次比较**当前元素（$a_i$）**和**前一个元素（$a_{i-1}$）**以及**前二个元素（$a_{i-2}$）**。但是这里应当循环比较。比如测试用例`9 5 6 9`，为了防止下标越界，我们从`a[2]`开始比较，比较到`a[3]`都是没有结果的，此时第一个元素`a[0]`和最后一个元素`a[3]`是相同，那么意味着算法不正确，但是如果是循环数组，那么就可以理解为这两个元素是`a[i]`和`a[i-1]`的关系。在具体语言中需要注意，Python中是默认有负索引的，所以`a[0]`可以和`a[-1]`及`a[-2]`进行比较，但是C/C++以及Java和其他语言可能就不行，此时要进行单独判断。