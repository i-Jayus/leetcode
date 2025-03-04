# [169. 多数元素](https://leetcode.cn/problems/majority-element)

[English Version](/solution/0100-0199/0169.Majority%20Element/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>给定一个大小为 <code>n</code><em> </em>的数组&nbsp;<code>nums</code> ，返回其中的多数元素。多数元素是指在数组中出现次数 <strong>大于</strong>&nbsp;<code>⌊ n/2 ⌋</code>&nbsp;的元素。</p>

<p>你可以假设数组是非空的，并且给定的数组总是存在多数元素。</p>

<p>&nbsp;</p>

<p><strong>示例&nbsp;1：</strong></p>

<pre>
<strong>输入：</strong>nums = [3,2,3]
<strong>输出：</strong>3</pre>

<p><strong>示例&nbsp;2：</strong></p>

<pre>
<strong>输入：</strong>nums = [2,2,1,1,1,2,2]
<strong>输出：</strong>2
</pre>

<p>&nbsp;</p>
<strong>提示：</strong>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 &lt;= n &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>-10<sup>9</sup> &lt;= nums[i] &lt;= 10<sup>9</sup></code></li>
</ul>

<p>&nbsp;</p>

<p><strong>进阶：</strong>尝试设计时间复杂度为 O(n)、空间复杂度为 O(1) 的算法解决此问题。</p>

## 解法

<!-- 这里可写通用的实现逻辑 -->

**方法一：摩尔投票法**

摩尔投票法的基本步骤如下：

初始化元素 $m$，并给计数器 $cnt$ 赋初值 $cnt=0$。对于输入列表中每一个元素 $x$：

1. 若 $cnt=0$，那么 $m=x$ and $cnt=1$；
1. 否则若 $m=x$，那么 $cnt=cnt+1$；
1. 否则 $cnt=cnt-1$。

一般而言，摩尔投票法需要对输入的列表进行**两次遍历**。在第一次遍历中，我们生成候选值 $m$，如果存在多数，那么该候选值就是多数值。在第二次遍历中，只需要简单地计算候选值的频率，以确认是否是多数值。由于本题已经明确说明存在多数值，所以第一次遍历结束后，直接返回 m 即可，无需二次遍历确认是否是多数值。

时间复杂度 $O(n)$，空间复杂度 $O(1)$。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        cnt = m = 0
        for v in nums:
            if cnt == 0:
                m, cnt = v, 1
            else:
                cnt += 1 if m == v else -1
        return m
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public int majorityElement(int[] nums) {
        int cnt = 0, m = 0;
        for (int v : nums) {
            if (cnt == 0) {
                m = v;
                cnt = 1;
            } else {
                cnt += (m == v ? 1 : -1);
            }
        }
        return m;
    }
}
```

### **JavaScript**

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function (nums) {
    let cnt = 0,
        m = 0;
    for (const v of nums) {
        if (cnt == 0) {
            m = v;
            cnt = 1;
        } else {
            cnt += m == v ? 1 : -1;
        }
    }
    return m;
};
```

### **C++**

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int cnt = 0, m = 0;
        for (int& v : nums) {
            if (cnt == 0) {
                m = v;
                cnt = 1;
            } else
                cnt += (m == v ? 1 : -1);
        }
        return m;
    }
};
```

### **C#**

```cs
public class Solution {
    public int MajorityElement(int[] nums) {
        int cnt = 0, m = 0;
        foreach (int v in nums)
        {
            if (cnt == 0)
            {
                m = v;
                cnt = 1;
            }
            else
            {
                cnt += m == v ? 1 : -1;
            }
        }
        return m;
    }
}
```

### **Go**

```go
func majorityElement(nums []int) int {
	cnt, m := 0, 0
	for _, v := range nums {
		if cnt == 0 {
			m, cnt = v, 1
		} else {
			if m == v {
				cnt++
			} else {
				cnt--
			}
		}
	}
	return m
}
```

### **Rust**

```rust
impl Solution {
    pub fn majority_element(nums: Vec<i32>) -> i32 {
        let mut m = 0;
        let mut cnt = 0;
        for &v in nums.iter() {
            if cnt == 0 {
                m = v;
                cnt = 1;
            } else {
                cnt += if m == v { 1 } else { -1 };
            }
        }
        m
    }
}
```

### **PHP**

```php
class Solution {
    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function majorityElement($nums) {
        $major = 0;
        $count = 0;
        for ($i = 0; $i < count($nums); $i++) {
            if ($count == 0) $major = $nums[$i];
            if ($major == $nums[$i]) $count++;
            else $count--;
        }
        return $major;
    }
}
```

### **...**

```

```

<!-- tabs:end -->
