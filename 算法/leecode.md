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





```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
    
        k = nums.length - k;
        int l = 0;
        int r = nums.length - 1;
        quickSort(nums,l,r,k);
        return nums[k];
    }

    public void quickSort(int[] nums, int l, int r, int k) {
        if (l < r) {
            int[] p = partition(nums,l,r);
            if (k > p[0] + 1) {
                quickSort(nums, p[0] + 2, r, k);
            } else if (k < p[0] + 1) {
                quickSort(nums, l, p[0], k);
            } else {
                return;
            }
        }
    }

     

    public int[] partition(int[] nums, int l, int r) {
        int less = l - 1;
        int more = r;
        while (l < more) {
            if (nums[l] < nums[r]) {
                swap(nums, ++less, l++);
            } else if (nums[l] > nums[r]) {
                swap(nums, l, --more);
            } else {
                l++;
            }
        }
        swap(nums, more, r);
        return new int[]{less, more + 1};
    }

    public void swap(int[] nums, int i, int j) {
        if (i == j) {
            return;
        }
        nums[i] = nums[i] ^ nums[j];
        nums[j] = nums[i] ^ nums[j];
        nums[i] = nums[i] ^ nums[j];
    }
}
```



#### [347. 前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)

难度中等619

给定一个非空的整数数组，返回其中出现频率前 ***k\*** 高的元素。

 

**示例 1:**

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```

**示例 2:**

```
输入: nums = [1], k = 1
输出: [1]
```

 

**提示：**

- 你可以假设给定的 *k* 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
- 你的算法的时间复杂度**必须**优于 O(*n* log *n*) , *n* 是数组的大小。
- 题目数据保证答案唯一，换句话说，数组中前 k 个高频元素的集合是唯一的。
- 你可以按任意顺序返回答案。

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> frequentForNum = new HashMap<>();
        for (int num: nums) {
            frequentForNum.put(num, frequentForNum.getOrDefault(num, 0) + 1);
        }
        ArrayList<Integer>[] buckets = new ArrayList[nums.length + 1];
        for (int key: frequentForNum.keySet()) {
            int frequent = frequentForNum.get(key);
            if (buckets[frequent] == null) {
                buckets[frequent] = new ArrayList<Integer>();
            }
            buckets[frequent].add(key);
        }
        List<Integer> topK = new ArrayList<>();
        for (int i = buckets.length - 1; topK.size() < k && i >= 0; i-- ) {
            if (buckets[i] == null) {
                continue;
            }
            if (buckets[i].size() < (k - topK.size())) {
                topK.addAll(buckets[i]);
            } else {
                topK.addAll(buckets[i].subList(0,k - topK.size()));
            }
        }
        int[] res = new int[k];
        for (int i = 0;i < k;i++) {
            res[i] = topK.get(i);
        }
        return res;
    }
}
```

arr.length

List<Integer>[] arr = new ArrayList[10];// 不需要添加<>





#### [451. 根据字符出现频率排序](https://leetcode-cn.com/problems/sort-characters-by-frequency/)

难度中等205

给定一个字符串，请将字符串里的字符按照出现的频率降序排列。

**示例 1:**

```
输入:
"tree"

输出:
"eert"

解释:
'e'出现两次，'r'和't'都只出现一次。
因此'e'必须出现在'r'和't'之前。此外，"eetr"也是一个有效的答案。
```





```java
class Solution {
    public String frequencySort(String s) {
        Map<Character, Integer> frequencyForNum = new HashMap<>();
        char[] sArr = s.toCharArray();
        for (char c: s.toCharArray()) {
            frequencyForNum.put(c, frequencyForNum.getOrDefault(c, 0) + 1);
            
        }
        List<Character>[] buckets = new ArrayList[sArr.length + 1];
        for (char c: frequencyForNum.keySet()) {
            int size = frequencyForNum.get(c);
            if (buckets[size] == null) {
                buckets[size] = new ArrayList<>();
            }
            buckets[size].add(c);
        }
        StringBuilder sb = new StringBuilder();
        for (int i = buckets.length - 1; i >= 0; i--) {
            if (buckets[i] == null) {
                continue;
            }
            for (char c: buckets[i]){
                for (int j = 0; j < i; j++) { // 出现多次
                    sb.append(c);
                }
                
            }
        }
        return sb.toString();

    }
}
```

#### [75. 颜色分类](https://leetcode-cn.com/problems/sort-colors/)

难度中等761

给定一个包含红色、白色和蓝色，一共 `n` 个元素的数组，**[原地](https://baike.baidu.com/item/原地算法)**对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 `0`、 `1` 和 `2` 分别表示红色、白色和蓝色。



 

**示例 1：**

```
输入：nums = [2,0,2,1,1,0]
输出：[0,0,1,1,2,2]
```

**示例 2：**

```
输入：nums = [2,0,1]
输出：[0,1,2]
```

**示例 3：**

```
输入：nums = [0]
输出：[0]
```

**示例 4：**

```
输入：nums = [1]
输出：[1]
```

 

**提示：**

- `n == nums.length`
- `1 <= n <= 300`
- `nums[i]` 为 `0`、`1` 或 `2`

 

**进阶：**

- 你可以不使用代码库中的排序函数来解决这道题吗？
- 你能想出一个仅使用常数空间的一趟扫描算法吗？

```java
class Solution {
    public void sortColors(int[] nums) {
        int l = -1;
        int r = nums.length;
        int i = 0;
        while (i < r) {
            if (nums[i] == 0) {
                swap(nums, ++l, i++);
            } else if (nums[i] == 2) {
                swap(nums, i, --r);
            } else {
                i++;
            }
        }
    }

    public void swap(int[] nums, int i, int j) {
        if (i == j) {
            return;
        }
        nums[i] = nums[i] ^ nums[j];
        nums[j] = nums[i] ^ nums[j];
        nums[i] = nums[i] ^ nums[j];
    }
}
```

### 二分查找

#### [1. x 的平方根](https://leetcode-cn.com/problems/sqrtx/)

难度简单576

实现 `int sqrt(int x)` 函数。

计算并返回 *x* 的平方根，其中 *x* 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

**示例 1:**

```
输入: 4
输出: 2
```

**示例 2:**

```
输入: 8
输出: 2
说明: 8 的平方根是 2.82842..., 
     由于返回类型是整数，小数部分将被舍去。
```



```java
class Solution {
    public int mySqrt(int x) {
        if (x <= 1) {
            return x;
        }
        int l = 1;
        int r = x;
        
        while (l <= r) {   // 相等仍要判断
            int mid = l + (r - l) / 2;
            int sqrt = x / mid;
            if (sqrt == mid) {
                return mid;
            } else if (sqrt > mid) {
                l = mid + 1;
            } else {
                r = mid - 1; // 大于
            }
        }
        return r;
    }
}
```

```java
 public static double mySqrt(int x) {

        if (x <= 1) {
            return x;
        }
        double l = 1;
        double r = x;
        while (Math.abs(l - r) >= 1e-5) { 
            double mid = l + (r - l) / 2;
            double sqrt = x / mid;
            if (sqrt == mid) {
                return sqrt;
            } else if (sqrt > mid) {   // 说明mid*mid < x,所以变大
                l = mid;
            } else {
                r = mid;
            }
        }

        return r;
    }

    public static void main(String[] args) {
        double v = mySqrt(4);
        System.out.println(v);
        System.out.println(String.format("%.6f",v));

    }
```





#### [2. 寻找比目标字母大的最小字母](https://leetcode-cn.com/problems/find-smallest-letter-greater-than-target/)

难度简单110

给你一个排序后的字符列表 `letters` ，列表中只包含小写英文字母。另给出一个目标字母 `target`，请你寻找在这一有序列表里比目标字母大的最小字母。

在比较时，字母是依序循环出现的。举个例子：

- 如果目标字母 `target = 'z'` 并且字符列表为 `letters = ['a', 'b']`，则答案返回 `'a'`

 

**示例：**

```
输入:
letters = ["c", "f", "j"]
target = "a"
输出: "c"

输入:
letters = ["c", "f", "j"]
target = "c"
输出: "f"
```

 

**提示：**

1. `letters`长度范围在`[2, 10000]`区间内。
2. `letters` 仅由小写字母组成，最少包含两个不同的字母。
3. 目标字母`target` 是一个小写字母。



找不到则返回第一个字符

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int l = 0;
        int r = letters.length - 1;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (letters[mid] <= target) {
                l = mid + 1;
            } else {
                r = mid - 1;
            }
        }

      
        return l < letters.length ? letters[l] : letters[0];

    }
}
```



#### [3. 有序数组中的单一元素](https://leetcode-cn.com/problems/single-element-in-a-sorted-array/)

难度中等189

给定一个只包含整数的有序数组，每个元素都会出现两次，唯有一个数只会出现一次，找出这个数。

**示例 1:**

```
输入: [1,1,2,3,3,4,4,8,8]
输出: 2
```

**示例 2:**

```
输入: [3,3,7,7,10,11,11]
输出: 10
```

**注意:** 您的方案应该在 O(log n)时间复杂度和 O(1)空间复杂度中运行。







```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int l = 0;
        int  r = nums.length - 1;
        while (l < r) {
            int mid = l + (r - l) / 2;
            if (mid % 2 == 1) {
                mid--;
            }
            if (nums[mid] == nums[mid + 1]) {
                l = mid + 2;
            } else {
                r = mid;
            }
        }
        return nums[l];
    }
}
```

#### [4. 第一个错误的版本](https://leetcode-cn.com/problems/first-bad-version/)

难度简单253

你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。

假设你有 `n` 个版本 `[1, 2, ..., n]`，你想找出导致之后所有版本出错的第一个错误的版本。

你可以通过调用 `bool isBadVersion(version)` 接口来判断版本号 `version` 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数。

**示例:**

```
给定 n = 5，并且 version = 4 是第一个错误的版本。

调用 isBadVersion(3) -> false
调用 isBadVersion(5) -> true
调用 isBadVersion(4) -> true
```



```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        // bool isBadVersion(version)
        int l = 1;
        int r = n;
        while (l < r) {
            int m = l + (r - l) / 2;
            if (isBadVersion(m)){
                r = m;
            } else {
                l = m + 1;
            }
        }
        return l == n + 1 ? -1 : l;
    }
}
```





#### [5. 寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

难度中等333

假设按照升序排序的数组在预先未知的某个点上进行了旋转。例如，数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]` 。

请找出其中最小的元素。

 

**示例 1：**

```
输入：nums = [3,4,5,1,2]
输出：1
```

**示例 2：**

```
输入：nums = [4,5,6,7,0,1,2]
输出：0
```

**示例 3：**

```
输入：nums = [1]
输出：1
```

 

**提示：**

- `1 <= nums.length <= 5000`
- `-5000 <= nums[i] <= 5000`
- `nums` 中的所有整数都是 **唯一** 的
- `nums` 原来是一个升序排序的数组，但在预先未知的某个点上进行了旋转



```java
class Solution {
    public int findMin(int[] nums) {
        int l = 0;
        int r = nums.length - 1;
        while (l < r) {
            int m = l + (r - l) / 2;
            if (nums[m] <= nums[r]) {
                r = m;
            } else {
                l = m + 1;
            }
        }
        return nums[l];
    }
}
```

#### [6. 在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

难度中等823

给定一个按照升序排列的整数数组 `nums`，和一个目标值 `target`。找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 `target`，返回 `[-1, -1]`。

**进阶：**

- 你可以设计并实现时间复杂度为 `O(log n)` 的算法解决此问题吗？

 

**示例 1：**

```
输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]
```

**示例 2：**

```
输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]
```

**示例 3：**

```
输入：nums = [], target = 0
输出：[-1,-1]
```

 

**提示：**

- `0 <= nums.length <= 105`
- `-109 <= nums[i] <= 109`
- `nums` 是一个非递减数组
- `-109 <= target <= 109`



```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        
        int f = findFirst(nums,target);
        int l = findFirst(nums,target + 1) - 1;
        if (f == nums.length || nums[f] != target) {
            return new int[]{-1, -1};
        }
        return new int[]{f, Math.max(f,l)};
    }


    private int findFirst(int[] nums, int target) {
        int l = 0;
        int r = nums.length;  // [2, 2]  3 ->2
        while (l < r) {
            int m = l + (r - l) / 2;
            if (nums[m] >= target) {
                r = m;
            } else {
                l = m + 1;
            }
        }
        return l;
    }
}
```

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210126151258.png)



### 分治

#### [241. 为运算表达式设计优先级](https://leetcode-cn.com/problems/different-ways-to-add-parentheses/)

难度中等319

给定一个含有数字和运算符的字符串，为表达式添加括号，改变其运算优先级以求出不同的结果。你需要给出所有可能的组合的结果。有效的运算符号包含 `+`, `-` 以及 `*` 。

**示例 1:**

```
输入: "2-1-1"
输出: [0, 2]
解释: 
((2-1)-1) = 0 
(2-(1-1)) = 2
```

**示例 2:**

```
输入: "2*3-4*5"
输出: [-34, -14, -10, -10, 10]
解释: 
(2*(3-(4*5))) = -34 
((2*3)-(4*5)) = -14 
((2*(3-4))*5) = -10 
(2*((3-4)*5)) = -10 
(((2*3)-4)*5) = 10
```



```java
class Solution {
    public List<Integer> diffWaysToCompute(String input) {
        List<Integer> ways = new ArrayList<>();
        for (int i = 0; i < input.length(); i++) {
            char ch = input.charAt(i);
            if (ch == '+' || ch == '-' || ch == '*') {
                List<Integer> left = diffWaysToCompute(input.substring(0, i));
                List<Integer> right = diffWaysToCompute(input.substring(i + 1));
                for (int l : left) {
                    for (int r : right) {
                        switch(ch){
                            case '+':
                                ways.add(l + r);
                                break;
                            case '-':
                                ways.add(l - r);
                                break;
                            case '*':
                                ways.add(l * r);
                                break;
                        }
                    }
                }

            }
        }
        if (ways.size() == 0) {
            ways.add(Integer.valueOf(input));
        }
        return ways;
    }
}
```

#### [95. 不同的二叉搜索树 II](https://leetcode-cn.com/problems/unique-binary-search-trees-ii/)

难度中等768

给定一个整数 *n*，生成所有由 1 ... *n* 为节点所组成的 **二叉搜索树** 。

 

**示例：**

```
输入：3
输出：
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释：
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

 

**提示：**

- `0 <= n <= 8`



```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<TreeNode> generateTrees(int n) {
        if (n < 1) {
            return new ArrayList<TreeNode>();
        }
        return generateSubtrees(1, n);
    }

    public List<TreeNode> generateSubtrees(int s, int e) {
        List<TreeNode> res = new LinkedList<TreeNode>();
        if (s > e) {
            res.add(null);
            return res;
        }
        for (int i = s; i <= e; i++) {
            List<TreeNode> left  = generateSubtrees(s, i - 1);
            List<TreeNode> right = generateSubtrees(i + 1, e);
            for (TreeNode l : left) {
                for (TreeNode r : right) {
                    TreeNode node = new TreeNode(i);
                    node.left = l;
                    node.right = r;
                    res.add(node);
                }
            }
        }
        return res;
    }

}
```











### BFS

#### [1. 二进制矩阵中的最短路径](https://leetcode-cn.com/problems/shortest-path-in-binary-matrix/)

难度中等

在一个 N × N 的方形网格中，每个单元格有两种状态：空（0）或者阻塞（1）。

一条从左上角到右下角、长度为 `k` 的畅通路径，由满足下述条件的单元格 `C_1, C_2, ..., C_k` 组成：

- 相邻单元格 `C_i` 和 `C_{i+1}` 在八个方向之一上连通（此时，`C_i` 和 `C_{i+1}` 不同且共享边或角）
- `C_1` 位于 `(0, 0)`（即，值为 `grid[0][0]`）
- `C_k` 位于 `(N-1, N-1)`（即，值为 `grid[N-1][N-1]`）
- 如果 `C_i` 位于 `(r, c)`，则 `grid[r][c]` 为空（即，`grid[r][c] == 0`）

返回这条从左上角到右下角的最短畅通路径的长度。如果不存在这样的路径，返回 -1 。

 

**示例 1：**

```
输入：[[0,1],[1,0]]

输出：2
```

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210127114924.png)





```java
class Solution {
    public int shortestPathBinaryMatrix(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return -1;
        }
        int[][] direction = {{-1, 0}, {0, 1}, {1, 0}, {0, -1}, {-1, 1}, {1, 1}, {1, -1}, {-1, -1}};
        int pathLength = 0;
        int m = grid.length;
        int n = grid[0].length;
        Queue<Pair<Integer, Integer>> queue = new LinkedList<>();
        queue.offer(new Pair(0, 0));
        while (!queue.isEmpty()) {
            int size = queue.size();
            pathLength++;
            while (size-- > 0) {
                Pair<Integer, Integer> pair = queue.poll();
                int cr = pair.getKey();
                int cc = pair.getValue();
                if (grid[cr][cc] == 1) {
                    continue;
                }
                if (cr == m - 1 && cc == n - 1) {
                    return pathLength;
                }
                grid[cr][cc] = 1;
                for (int[] d : direction) {
                    int nr = cr + d[0];
                    int nc = cc + d[1];
                    if (nr < 0 || nr >= m || nc < 0 || nc >= n) {
                        continue;
                    }
                    queue.offer(new Pair(nr, nc));
                }
            }
        }
        return -1;

    }
}
```

#### [279. 完全平方数](https://leetcode-cn.com/problems/perfect-squares/)

难度中等742

给定正整数 *n*，找到若干个完全平方数（比如 `1, 4, 9, 16, ...`）使得它们的和等于 *n*。你需要让组成和的完全平方数的个数最少。

给你一个整数 `n` ，返回和为 `n` 的完全平方数的 **最少数量** 。

**完全平方数** 是一个整数，其值等于另一个整数的平方；换句话说，其值等于一个整数自乘的积。例如，`1`、`4`、`9` 和 `16` 都是完全平方数，而 `3` 和 `11` 不是。

 

**示例 1：**

```
输入：n = 12
输出：3 
解释：12 = 4 + 4 + 4
```

**示例 2：**

```
输入：n = 13
输出：2
解释：13 = 4 + 9
```

**提示：**

- `1 <= n <= 104`



```java
class Solution {
    public int numSquares(int n) {
        List<Integer> squares = generateSquares(n);
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(n);
        int level = 0;
        boolean[] hasVisited = new boolean[n + 1];
        hasVisited[n] = true;
        while (!queue.isEmpty()) {
            int size = queue.size();
            level++;
            while (size-- > 0) {
                int cur = queue.poll();
                for (int s : squares) {
                    int next = cur - s;
                    if (next < 0) {
                        break;
                    }
                    if (next == 0) {
                        return level;
                    }
                    if (hasVisited[next]) {
                        continue;
                    }
                    hasVisited[next] = true;
                    queue.offer(next);
                }
            }
        }
        return n;

    }

     public List<Integer> generateSquares(int n) {
        List<Integer> squares = new ArrayList<>();
        int square = 1;
        int diff = 3;
        while (square <= n) {
            squares.add(square);
            square += diff;
            diff += 2;
        }
        return squares;
    }
}
```





#### [127. 单词接龙](https://leetcode-cn.com/problems/word-ladder/)

难度困难685

字典 `wordList` 中从单词 `beginWord` 和 `endWord` 的 **转换序列** 是一个按下述规格形成的序列：

- 序列中第一个单词是 `beginWord` 。
- 序列中最后一个单词是 `endWord` 。
- 每次转换只能改变一个字母。
- 转换过程中的中间单词必须是字典 `wordList` 中的单词。

给你两个单词 `beginWord` 和 `endWord` 和一个字典 `wordList` ，找到从 `beginWord` 到 `endWord` 的 **最短转换序列** 中的 **单词数目** 。如果不存在这样的转换序列，返回 0。

**示例 1：**

```
输入：beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
输出：5
解释：一个最短转换序列是 "hit" -> "hot" -> "dot" -> "dog" -> "cog", 返回它的长度 5。
```

**示例 2：**

```
输入：beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
输出：0
解释：endWord "cog" 不在字典中，所以无法进行转换。
```

 

**提示：**

- `1 <= beginWord.length <= 10`
- `endWord.length == beginWord.length`
- `1 <= wordList.length <= 5000`
- `wordList[i].length == beginWord.length`
- `beginWord`、`endWord` 和 `wordList[i]` 由小写英文字母组成
- `beginWord != endWord`
- `wordList` 中的所有字符串 **互不相同**



```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        wordList.add(beginWord);
        int N = wordList.size();
        int start = N - 1;
        int end = 0;
        while (end < N && !wordList.get(end).equals(endWord)) {
            end++;
        }
        if (end == N) {
            return 0;
        }
        List<Integer>[] graphics = buildGraphic(wordList);
        return getShortestPath(start, end, graphics);
    }

    public List<Integer>[] buildGraphic(List<String> wordList) {
        int N = wordList.size();
        List<Integer>[] graphics = new ArrayList[N];
        for (int i = 0; i < N; i++) {
            graphics[i] = new ArrayList<Integer>();
            for (int j = 0; j < N; j++) {
                if (isConnect(wordList.get(i), wordList.get(j))) {
                    graphics[i].add(j);
                }
            }
        }
        return graphics;

    }

    public boolean isConnect(String str1, String str2) {
        
        int diffCnt = 0;
        for (int i = 0; i < str1.length() && diffCnt <= 1; i++) {
            if (str1.charAt(i) != str2.charAt(i)) {
                diffCnt++;
            }
        }
        return diffCnt == 1;
    }

    public int getShortestPath(int start, int end, List<Integer>[] graphics) {

        Queue<Integer> queue = new LinkedList<>();
        queue.offer(start);
        int N = graphics.length;
        boolean[] hasVisited = new boolean[N];
        hasVisited[start] = true;
        int level = 1;
        while (!queue.isEmpty()) {
            int size = queue.size();
            level++;
            while (size-- > 0) {
                int cur = queue.poll();
                for (int next : graphics[cur]) {
                    if (next == end) {
                        return level;
                    }
                    if (hasVisited[next]) {
                        continue;
                    }
                    hasVisited[next] = true;
                    queue.offer(next);
                }

            }
        }
        return 0;
    }
    
}
```



### DFS

#### [695. 岛屿的最大面积](https://leetcode-cn.com/problems/max-area-of-island/)

难度中等422

给定一个包含了一些 `0` 和 `1` 的非空二维数组 `grid` 。

一个 **岛屿** 是由一些相邻的 `1` (代表土地) 构成的组合，这里的「相邻」要求两个 `1` 必须在水平或者竖直方向上相邻。你可以假设 `grid` 的四个边缘都被 `0`（代表水）包围着。

找到给定的二维数组中最大的岛屿面积。(如果没有岛屿，则返回面积为 `0` 。)

 

**示例 1:**

```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
```

对于上面这个给定矩阵应返回 `6`。注意答案不应该是 `11` ，因为岛屿只能包含水平或垂直的四个方向的 `1` 。

**示例 2:**

```
[[0,0,0,0,0,0,0,0]]
```

对于上面这个给定的矩阵, 返回 `0`。





```java
class Solution {

    private int m;
    private int n;
    private int[][] direction = {{-1, 0}, {0, 1}, {1, 0}, {0, -1}};

    public int maxAreaOfIsland(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        int maxArea = 0;
        m = grid.length;
        n = grid[0].length;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                maxArea = Math.max(maxArea, dfs(grid, i, j));
            }
        }
        return maxArea;
    }

    private int dfs(int[][] grid, int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >=n || grid[i][j] == 0) {
            return 0;
        }

        int area = 1;
        grid[i][j] = 0;
        for (int[] d : direction) {
            area += dfs(grid, i + d[0], j + d[1]);
        }
        return area;
        

    }
}
```

#### [200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

难度中等959

给你一个由 `'1'`（陆地）和 `'0'`（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向和/或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。

 

**示例 1：**

```
输入：grid = [
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
输出：1
```

**示例 2：**

```
输入：grid = [
  ["1","1","0","0","0"],
  ["1","1","0","0","0"],
  ["0","0","1","0","0"],
  ["0","0","0","1","1"]
]
输出：3
```

 

**提示：**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 300`
- `grid[i][j]` 的值为 `'0'` 或 `'1'`



```java
class Solution {

    private int m;
    private int n;
    private int[][] direction = {{-1, 0}, {0, 1}, {1, 0}, {0, -1}};

    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        m = grid.length;
        n = grid[0].length;
        int islandsNum = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == '1') {
                    dfs(grid, i, j);
                    islandsNum++;
                }
            }
        }
        return islandsNum;
    }

    public void dfs(char[][] grid, int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] == '0') {
            return;
        }
        grid[i][j] = '0';
        for (int[] d : direction) {
            dfs(grid, i + d[0], j + d[1]);
        }
    }

}
```





#### [547. 省份数量](https://leetcode-cn.com/problems/number-of-provinces/)

难度中等482

有 `n` 个城市，其中一些彼此相连，另一些没有相连。如果城市 `a` 与城市 `b` 直接相连，且城市 `b` 与城市 `c` 直接相连，那么城市 `a` 与城市 `c` 间接相连。

**省份** 是一组直接或间接相连的城市，组内不含其他没有相连的城市。

给你一个 `n x n` 的矩阵 `isConnected` ，其中 `isConnected[i][j] = 1` 表示第 `i` 个城市和第 `j` 个城市直接相连，而 `isConnected[i][j] = 0` 表示二者不直接相连。

返回矩阵中 **省份** 的数量。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)

```
输入：isConnected = [[1,1,0],[1,1,0],[0,0,1]]
输出：2
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg)

```
输入：isConnected = [[1,0,0],[0,1,0],[0,0,1]]
输出：3
```

 

**提示：**

- `1 <= n <= 200`
- `n == isConnected.length`
- `n == isConnected[i].length`
- `isConnected[i][j]` 为 `1` 或 `0`
- `isConnected[i][i] == 1`
- `isConnected[i][j] == isConnected[j][i]`



```java
class Solution {

    private int n;

    public int findCircleNum(int[][] isConnected) {
        if (isConnected == null || isConnected.length == 0 || isConnected[0].length == 0) {
            return 0;
        }
        n = isConnected.length;
        boolean[] hasVisited = new boolean[n];
        int circleNum = 0;
        for (int i = 0; i < n; i++) {
            if (!hasVisited[i]) {
                dfs(isConnected, i, hasVisited);
                circleNum++;
            }
        }
        return circleNum;
    }

    public void dfs(int[][] isConnected, int i, boolean[] hasVisited) {

        hasVisited[i] = true;
        for (int j = 0; j < n; j++) {
            if (isConnected[i][j] == 1 && !hasVisited[j]) {
                dfs(isConnected, j, hasVisited);
            }
        }
    }
}
```





### end