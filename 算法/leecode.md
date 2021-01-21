### 双指针

#### [167. 两数之和 II - 输入有序数组](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

给定一个已按照***升序排列\*** 的有序数组，找到两个数使得它们相加之和等于目标数。

函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2*。*

**说明:**

- 返回的下标值（index1 和 index2）不是从零开始的。
- 你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

**示例:**

```
输入: numbers = [2, 7, 11, 15], target = 9
输出: [1,2]
解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。
```



```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int len  = numbers.length;

        int l = 0;
        int r = len - 1;
        int sum = 0;
        while (l < r) {
            sum = numbers[l] + numbers [r];
            if (sum == target) {
                return new int[]{l+1, r+ 1};
            } else if (sum > target) {
                r--;
            } else {
                l++;
            }
        }
        return new int[]{-1, -1};
    }
}
```

```java
public int[] twoSum(int[] numbers, int target) {
    if (numbers == null) return null;
    int i = 0, j = numbers.length - 1;
    while (i < j) {
        int sum = numbers[i] + numbers[j];
        if (sum == target) {
            return new int[]{i + 1, j + 1};
        } else if (sum < target) {
            i++;
        } else {
            j--;
        }
    }
    return null;
}
```

#### [633. 平方数之和](https://leetcode-cn.com/problems/sum-of-square-numbers/)

难度中等161

给定一个非负整数 `c` ，你要判断是否存在两个整数 `a` 和 `b`，使得 `a2 + b2 = c` 。

 

**示例 1：**

```
输入：c = 5
输出：true
解释：1 * 1 + 2 * 2 = 5
```

**示例 2：**

```
输入：c = 3
输出：false
```

**示例 3：**

```
输入：c = 4
输出：true
```

**示例 4：**

```
输入：c = 2
输出：true
```

**示例 5：**

```
输入：c = 1
输出：true
```

 

**提示：**

- `0 <= c <= 2^31 - 1`

```java
class Solution {
    public boolean judgeSquareSum(int c) {
        if (c < 0) {
            return false;
        }
        int l = 0;
        int r = (int) Math.sqrt(c); // 
        int result = 0;
        while (l <= r) {
            result = l * l + r * r;
            if (result == c) {
                return true;
            } else if (result > c) {
                r--;
            } else {
                l++;
            }
        }
        return false;
    }
}
```

不使用平方根会超出int的范围





#### [345. 反转字符串中的元音字母](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)

难度简单137

编写一个函数，以字符串作为输入，反转该字符串中的元音字母。

 

**示例 1：**

```
输入："hello"
输出："holle"
```

**示例 2：**

```
输入："leetcode"
输出："leotcede"
```

 

**提示：**

- 元音字母不包含字母 "y" 。

```java
class Solution {

    private static final HashSet<Character> values = new HashSet<>(
        Arrays.asList('a', 'o', 'e', 'i', 'u', 'A', 'O', 'E', 'I', 'U')
    ); 

    public String reverseVowels(String s) {
        if (s == null) {
            return s;
        }
        int l = 0;
        int r = s.length() - 1;
        char[] res = new char[s.length()];
        while (l <= r) {

            char cl = s.charAt(l);
            char cr = s.charAt(r);
            
            if (!values.contains(cl)) {
                res[l++] = cl;
            } else if (!values.contains(cr)) {
                res[r--] = cr;
            } else {
                res[l++] = cr;
                res[r--] = cl;
            }
        }
        return new String(res);
    }
}
```



#### [680. 验证回文字符串 Ⅱ](https://leetcode-cn.com/problems/valid-palindrome-ii/)

难度简单310

给定一个非空字符串 `s`，**最多**删除一个字符。判断是否能成为回文字符串。

**示例 1:**

```
输入: "aba"
输出: True
```

**示例 2:**

```
输入: "abca"
输出: True
解释: 你可以删除c字符。
```

**注意:**

1. 字符串只包含从 a-z 的小写字母。字符串的最大长度是50000。



```java
class Solution {
    public boolean validPalindrome(String s) {
        int l = 0;
        int r = s.length() - 1;
        for (;l < r;l++, r--){
            if (s.charAt(l) != s.charAt(r)) {
                return isPalindrome(s, l + 1, r) || isPalindrome(s, l, r - 1);
            }
        }
        return true;
    }

    public boolean isPalindrome(String s, int l, int r) {
        while (l < r) {
            if (s.charAt(l++) != s.charAt(r--)) {
                return false;
            }
            
        }
        return true;
    }
}
```



#### [88. 合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)

难度简单738

给你两个有序整数数组 `nums1` 和 `nums2`，请你将 `nums2` 合并到 `nums1` 中*，*使 `nums1` 成为一个有序数组。

初始化 `nums1` 和 `nums2` 的元素数量分别为 `m` 和 `n` 。你可以假设 `nums1` 有足够的空间（空间大小等于 `m + n`）来保存 `nums2` 中的元素。

 

**示例 1：**

```
输入：nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
输出：[1,2,2,3,5,6]
```

**示例 2：**

```
输入：nums1 = [1], m = 1, nums2 = [], n = 0
输出：[1]
```

 

**提示：**

- `0 <= m, n <= 200`
- `1 <= m + n <= 200`
- `nums1.length == m + n`
- `nums2.length == n`
- `-109 <= nums1[i], nums2[i] <= 109`

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int indexMerge = m + n - 1;
        int l1 = m - 1;
        int l2 = n - 1;
        while (l1 >= 0 || l2 >= 0) {
            if (l1 < 0) {
                nums1[indexMerge--] = nums2[l2--];
            } else if (l2 < 0) {
                nums1[indexMerge--] = nums1[l1--];
            } else if (nums1[l1] < nums2[l2]) {
                nums1[indexMerge--] = nums2[l2--];
            } else {
                nums1[indexMerge--] = nums1[l1--];
            }
        }
    }
}
```



#### [141. 环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)

难度简单909

给定一个链表，判断链表中是否有环。

如果链表中有某个节点，可以通过连续跟踪 `next` 指针再次到达，则链表中存在环。 为了表示给定链表中的环，我们使用整数 `pos` 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 `pos` 是 `-1`，则在该链表中没有环。**注意：`pos` 不作为参数进行传递**，仅仅是为了标识链表的实际情况。

如果链表中存在环，则返回 `true` 。 否则，返回 `false` 。

 

**进阶：**

你能用 *O(1)*（即，常量）内存解决此问题吗？



```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null) {
            return false;
        }
        ListNode fast = head.next;
        ListNode slow = head;

        while (fast != null && fast.next != null) {
             if (fast == slow) {
                return true;
            }
            fast = fast.next.next;
            slow = slow.next;
           
        }
        return false;
    }
}
```





#### [524. 通过删除字母匹配到字典里最长单词](https://leetcode-cn.com/problems/longest-word-in-dictionary-through-deleting/)

难度中等123

给定一个字符串和一个字符串字典，找到字典里面最长的字符串，该字符串可以通过删除给定字符串的某些字符来得到。如果答案不止一个，返回长度最长且字典顺序最小的字符串。如果答案不存在，则返回空字符串。

**示例 1:**

```
输入:
s = "abpcplea", d = ["ale","apple","monkey","plea"]

输出: 
"apple"
```

**示例 2:**

```
输入:
s = "abpcplea", d = ["a","b","c"]

输出: 
"a"
```

**说明:**

1. 所有输入的字符串只包含小写字母。
2. 字典的大小不会超过 1000。
3. 所有输入的字符串长度不会超过 1000。



```java
class Solution {
    public String findLongestWord(String s, List<String> d) {
        String longestWord = "";
        for (String target: d) {
            if (longestWord.length() > target.length() || (longestWord.length() == target.length()
                && longestWord.compareTo(target) < 0 )) {
                    continue;
            }
            if (isSubString(s, target)) {
                longestWord = target;
            }

        }
        return longestWord;
    }

    public boolean isSubString(String s, String target) {
        int l1 = 0;
        int l2 = 0;
        while (l1 < s.length() && l2 < target.length()) {
            if (s.charAt(l1) == target.charAt(l2)) {
                l2++;
            }
            l1++;
        }
        return l2 == target.length();
    }
}
```





### 排序

#### [215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

难度中等858

在未排序的数组中找到第 **k** 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

**示例 1:**

```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```

**示例 2:**

```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

**说明:**

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。





```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int num: nums) {
            pq.offer(num);
            if (pq.size() > k) {
                pq.poll();
            }
        }
        return pq.peek();
    }
}
```

