### 双指针

#### [1. 两数之和 II - 输入有序数组](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/)

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

#### [2. 平方数之和](https://leetcode-cn.com/problems/sum-of-square-numbers/)

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

**不使用平方根会超出int的范围**

l r -> 小于目标值移动左指针，大于目标值则移动右指针，和上一题是类似的



#### [3. 反转字符串中的元音字母](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)

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
    public String reverseVowels(String s) {
        
        Set<Character> set = new HashSet<>();
        set.add('a');
        set.add('o');
        set.add('e');
        set.add('i');
        set.add('u');
        set.add('A');
        set.add('O');
        set.add('E');
        set.add('I');
        set.add('U');
        if (s == null || s.length() == 0) {
            return s;
        }
        int l = 0;
        int r = s.length() - 1;
        char[] arr = s.toCharArray();
        while (l < r) {
            while (l< r && !set.contains(arr[l])){
                l++;
            }
            while (l< r && !set.contains(arr[r])){
                r--;
            }
            if (l >= r) {
                break;
            }
            swap(arr, l, r);
            l++;
            r--;

        }
        return new String(arr);


    }

    public void swap(char[] arr, int l, int r) {
        if (l == r) {
            return;
        }
        char t = arr[r];
        arr[r] = arr[l];
        arr[l] = t;
    }
}
```





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







#### [4. 验证回文字符串 Ⅱ](https://leetcode-cn.com/problems/valid-palindrome-ii/)



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



注意:使用i++,之后若使用i,需要注意



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





#### [7. 通过删除字母匹配到字典里最长单词](https://leetcode-cn.com/problems/longest-word-in-dictionary-through-deleting/)



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

#### 理论

一层一层遍历，每一层遍历上一层遍历的结果作为起点，每次遍历的节点是距离为1，且没有访问过。



*i节点先访问*

*di <= dj*



**使用队列存储结果**

**使用boolean数组标记已经被访问过的节点**



当层节点加入队列，判断当前队列的size,依次取出上层队列的节点， 遍历每个节点的时候以及将该节点可以访问距离为1的的所有节点且没有访问过加入队列。



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





先判断在输出



```java
if (grid[cr][cc] == 1) {
                    continue;
}
if (cr == m - 1 && cc == n - 1) {
    return pathLength;
}
```





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



##### 解决

判断list中是否有该元素

 ```java
if (end == N) {
      return 0;
}
 ```

list中每一个找到和它差一个元素的字符串，最后生成List<Integer>[],就会构成图，只需要bfs遍历该图即可





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

##### 解法

0 和 1都要计算，当前位置一直向后扩展



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



#### [130. 被围绕的区域](https://leetcode-cn.com/problems/surrounded-regions/)

难度中等464收藏分享切换为英文接收动态反馈

给定一个二维的矩阵，包含 `'X'` 和 `'O'`（**字母 O**）。

找到所有被 `'X'` 围绕的区域，并将这些区域里所有的 `'O'` 用 `'X'` 填充。

**示例:**

```
X X X X
X O O X
X X O X
X O X X
```

运行你的函数后，矩阵变为：

```
X X X X
X X X X
X X X X
X O X X
```

**解释:**

被围绕的区间不会存在于边界上，换句话说，任何边界上的 `'O'` 都不会被填充为 `'X'`。 任何不在边界上，或不与边界上的 `'O'` 相连的 `'O'` 最终都会被填充为 `'X'`。如果两个元素在水平或垂直方向相邻，则称它们是“相连”的。



```JAVA
class Solution {
    private int m;
    private int n;
    private int[][] direction = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};

    public void solve(char[][] board) {
        if (board == null || board.length == 0 || board[0].length == 0) {
            return;
        }
        m = board.length;
        n = board[0].length;

        for (int i = 0; i < m; i++) {
            dfs(i, 0, board);
            dfs(i, n - 1, board);
        }
        for (int i = 0; i < n; i++) {
            dfs(0, i, board);
            dfs(m - 1, i, board);
        }

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (board[i][j] == 'T') {
                    board[i][j] = 'O';
                } else if (board[i][j] == 'O') {
                    board[i][j] = 'X';
                }
            }
        }
    }

    private void dfs(int i, int j, char[][] board) {
        if (i < 0 || i >= m || j < 0 || j >=n || board[i][j] != 'O') {
            return;
        }
        board[i][j] = 'T';
        for (int[] d : direction) {
            dfs(i + d[0], j + d[1], board);
        }
    }

    
}
```





#### [417. 太平洋大西洋水流问题](https://leetcode-cn.com/problems/pacific-atlantic-water-flow/)

难度中等193

给定一个 `m x n` 的非负整数矩阵来表示一片大陆上各个单元格的高度。“太平洋”处于大陆的左边界和上边界，而“大西洋”处于大陆的右边界和下边界。

规定水流只能按照上、下、左、右四个方向流动，且只能从高到低或者在同等高度上流动。

请找出那些水流既可以流动到“太平洋”，又能流动到“大西洋”的陆地单元的坐标。

 

**提示：**

1. 输出坐标的顺序不重要
2. *m* 和 *n* 都小于150

 

**示例：**

 

```
给定下面的 5x5 矩阵:

  太平洋 ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * 大西洋

返回:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (上图中带括号的单元).
```

##### 解法

*当前位置已经设置就不怕其余元素破坏因为没有 false->true的设置*





```java
class Solution {

    private int m;
    private int n;
    private int[][] direction = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    private int[][] matrix;
    public List<List<Integer>> pacificAtlantic(int[][] matrix) {

        List<List<Integer>> res = new ArrayList<>();

        if (matrix == null || matrix.length == 0) {
            return res;
        }

        m = matrix.length;
        n = matrix[0].length;
        boolean[][] canReachT = new boolean[m][n];
        boolean[][] canReachB = new boolean[m][n];
        this.matrix = matrix;

        for (int i = 0; i < m; i++) {
            dfs(i, 0, canReachT);
            dfs(i, n - 1, canReachB);
        }

        for (int i = 0; i < n; i++) {
            dfs(0, i, canReachT);
            dfs(m - 1, i, canReachB);
        }

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (canReachT[i][j] && canReachB[i][j]) {
                    res.add(Arrays.asList(i, j));
                }
            }
        }
        return res;
        

    }

    public void dfs(int i, int j, boolean[][] canReach) {
        
        if (canReach[i][j]) {
            return;
        }
        canReach[i][j] = true;
        for (int[] d : direction) {
            int nextR = i + d[0];
            int nextC = j + d[1];
            if (nextR < 0 || nextR >= m || nextC < 0 || nextC >= n || 
                matrix[i][j] > matrix[nextR][nextC]) {
                    continue;
            }
            dfs(nextR, nextC, canReach);
        }
    }
}
```





### 回溯

#### [17. 电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

难度中等1111

给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。答案可以按 **任意顺序** 返回。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/original_images/17_telephone_keypad.png)

 

**示例 1：**

```
输入：digits = "23"
输出：["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

**示例 2：**

```
输入：digits = ""
输出：[]
```

**示例 3：**

```
输入：digits = "2"
输出：["a","b","c"]
```

 

**提示：**

- `0 <= digits.length <= 4`
- `digits[i]` 是范围 `['2', '9']` 的一个数字。



```java
class Solution {

    private final String[] KEYS = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    public List<String> letterCombinations(String digits) {
        List<String> combinations = new ArrayList<>();
        if (digits == null || digits.length() == 0) {
            return combinationList;
        }
        doCombinations(new StringBuilder(), digits, combinations);
        return combinationList;
    }

    public void doCombinations(StringBuilder prefix, String digits, List<String> combinations) {
        if (prefix.length() == digits.length()) {
            combinations.add(new String(prefix));
            return;
        }
        int curDigits = digits.charAt(prefix.length()) - '0';
        String letter = KEYS[curDigits];
        for (char ch : letter.toCharArray()) {
            prefix.append(ch);
            doCombinations(prefix,digits,combinations);
            prefix.deleteCharAt(prefix.length() - 1);
        }

    }

}
```



#### [93. 复原IP地址](https://leetcode-cn.com/problems/restore-ip-addresses/)

难度中等492

给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

**有效的 IP 地址** 正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 `0`），整数之间用 `'.' `分隔。

例如："0.1.2.201" 和 "192.168.1.1" 是 **有效的** IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是 **无效的** IP 地址。

 

**示例 1：**

```
输入：s = "25525511135"
输出：["255.255.11.135","255.255.111.35"]
```

**示例 2：**

```
输入：s = "0000"
输出：["0.0.0.0"]
```

**示例 3：**

```
输入：s = "1111"
输出：["1.1.1.1"]
```

**示例 4：**

```
输入：s = "010010"
输出：["0.10.0.10","0.100.1.0"]
```

**示例 5：**

```
输入：s = "101023"
输出：["1.0.10.23","1.0.102.3","10.1.0.23","10.10.2.3","101.0.2.3"]
```

 

**提示：**

- `0 <= s.length <= 3000`
- `s` 仅由数字组成



```java
class Solution {
    public List<String> restoreIpAddresses(String s) {

        List<String> address = new ArrayList<>();
        doRestore(0, new StringBuilder(), s, address);
        return address;

    }

    public void doRestore(int index, StringBuilder tempAddress, String s, List<String> address) {

        if (index == 4 || s.length() == 0) {
            if (index == 4 && s.length() == 0) {
                address.add(tempAddress.toString());
            }
            return;
        }

        for (int i = 0; i < s.length() && i <= 2; i++) {
            if (i != 0 && s.charAt(0) == '0') {
                break;
            }
            String part = s.substring(0, i + 1);
            if (Integer.valueOf(part) <= 255) {
                if (tempAddress.length() != 0) {
                    part = "." + part;
                }
                tempAddress.append(part);
                doRestore(index + 1, tempAddress, s.substring(i + 1), address);
                tempAddress.delete(tempAddress.length() - part.length(), tempAddress.length());
            }
            
        }

        
    }


}
```





#### [79. 单词搜索](https://leetcode-cn.com/problems/word-search/)

难度中等765

给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

 

**示例:**

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

给定 word = "ABCCED", 返回 true
给定 word = "SEE", 返回 true
给定 word = "ABCB", 返回 false
```

 

**提示：**

- `board` 和 `word` 中只包含大写和小写英文字母。
- `1 <= board.length <= 200`
- `1 <= board[i].length <= 200`
- `1 <= word.length <= 10^3`



```java
class Solution {

    private int[][] direction = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    private int m;
    private int n;

    public boolean exist(char[][] board, String word) {

        if (word == null || word.length() == 0) {
            return true;
        }

        if (board == null || board.length == 0 || board[0].length == 0) {
            return true;
        }
        m = board.length;
        n = board[0].length;
        boolean[][] hasVisited = new boolean[m][n];

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (backtracking(0, i, j, hasVisited, board, word)) {
                    return true;
                }
            }
        }
        return false;

    }

    public boolean backtracking(int curLen, int r, int c, boolean[][] hasVisited,
         char[][] board, String word) {
        
        if (curLen == word.length()) {
            return true;
        }
        if (r < 0 || r >= m || c < 0 || c >= n || board[r][c] != word.charAt(curLen) || hasVisited[r][c]) {
            return false;
        }
        hasVisited[r][c] = true;
        for (int[] d : direction) {

            if (backtracking(curLen + 1, r + d[0], c + d[1], hasVisited, board, word)) {
                return true;
            }
        }
        hasVisited[r][c] = false;
        return false;
    
    }



}
```

#### [257. 二叉树的所有路径](https://leetcode-cn.com/problems/binary-tree-paths/)

难度简单438

给定一个二叉树，返回所有从根节点到叶子节点的路径。

**说明:** 叶子节点是指没有子节点的节点。

**示例:**

```
输入:

   1
 /   \
2     3
 \
  5

输出: ["1->2->5", "1->3"]

解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3
```





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
    public List<String> binaryTreePaths(TreeNode root) {
        List<Integer> values = new ArrayList<>();
        List<String> paths = new ArrayList<>();
        backtracking(root, values, paths);
        return paths;
    }

    public void backtracking(TreeNode node, List<Integer> values, List<String> paths) {
        if (node == null) {
            return;
        }
        values.add(node.val);
        if (node.left == null && node.right == null) {
            paths.add(buildpath(values));
        } else {
            backtracking(node.left, values, paths);
            backtracking(node.right, values, paths);
        }
        values.remove(values.size() - 1);

    }

    public String buildpath(List<Integer> values) {
        StringBuilder stringBuilder = new StringBuilder();
        for (int i = 0; i < values.size(); i++) {
            stringBuilder.append(values.get(i));
            if (i != values.size() - 1) {
                stringBuilder.append("->");
            }
        }
        return stringBuilder.toString();
    }


}
```



#### [46. 全排列](https://leetcode-cn.com/problems/permutations/)

难度中等1107

给定一个 **没有重复** 数字的序列，返回其所有可能的全排列。

**示例:**

```
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```





```java

class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> permutes = new ArrayList<>();
        if (nums == null) {
            return permutes;
        }

        boolean[] hasVisited = new boolean[nums.length];
        backtracking(nums, new ArrayList<Integer>(), hasVisited, permutes);
        return permutes;
    }

    private void backtracking(int[] nums, List<Integer> tempPermutes, boolean[] hasVisited,
         List<List<Integer>> permutes) {
            
            if (tempPermutes.size() == nums.length) {
                permutes.add(new ArrayList<>(tempPermutes));
                return;
            }

            for (int i = 0; i < nums.length; i++) {
                if (hasVisited[i]) {
                    continue;
                }
                
                hasVisited[i] = true;
                tempPermutes.add(nums[i]);
                backtracking(nums, tempPermutes, hasVisited, permutes);
                hasVisited[i] = false;
                tempPermutes.remove(tempPermutes.size() - 1);
            }
    }
}
```



#### [47. 全排列 II](https://leetcode-cn.com/problems/permutations-ii/)

难度中等577

给定一个可包含重复数字的序列 `nums` ，**按任意顺序** 返回所有不重复的全排列。

 

**示例 1：**

```
输入：nums = [1,1,2]
输出：
[[1,1,2],
 [1,2,1],
 [2,1,1]]
```

**示例 2：**

```
输入：nums = [1,2,3]
输出：[[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

 

**提示：**

- `1 <= nums.length <= 8`
- `-10 <= nums[i] <= 10`







```java

class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {

        List<List<Integer>> permutes = new ArrayList<>();
        if (nums == null || nums.length == 0) {
            return permutes;
        }
        Arrays.sort(nums);
        boolean[] hasVisited = new boolean[nums.length];
        backtracking(nums, hasVisited, new ArrayList<Integer>(), permutes);
        return permutes;

    }


    private void backtracking(int[] nums, boolean[] hasVisited, List<Integer> tempPermute, 
        List<List<Integer>> permutes) {

            if (tempPermute.size() == nums.length) {
                permutes.add(new ArrayList<>(tempPermute));
                return;
            }

            for (int i = 0; i < nums.length; i++) {
                if (i != 0 && nums[i] == nums[i - 1] && !hasVisited[i - 1]) {
                    continue;
                }
                if (hasVisited[i]) {
                    continue;
                }
                hasVisited[i] = true;
                tempPermute.add(nums[i]);
                backtracking(nums, hasVisited, tempPermute, permutes);
                hasVisited[i] = false;
                tempPermute.remove(tempPermute.size() - 1);
            }

        }
}
```





#### [77. 组合](https://leetcode-cn.com/problems/combinations/)

难度中等480

给定两个整数 *n* 和 *k*，返回 1 ... *n* 中所有可能的 *k* 个数的组合。

**示例:**

```
输入: n = 4, k = 2
输出:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```





```java
class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> combines = new ArrayList<>();
        backtracking(1, n, k, new ArrayList<Integer>(), combines);
        return combines;
    }

    private void backtracking(int s, int n, int k, 
        List<Integer> tempCombine, List<List<Integer>> combines) {
            if (k == 0) {
                combines.add(new ArrayList(tempCombine));
                return;
            }

            for (int i = s; i <= n - k + 1; i++) {
                tempCombine.add(i);
                backtracking(i + 1, n, k - 1, tempCombine, combines);
                tempCombine.remove(tempCombine.size() - 1);
            }
        }
}
```





#### [39. 组合总和](https://leetcode-cn.com/problems/combination-sum/)

难度中等1150

给定一个**无重复元素**的数组 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的数字可以无限制重复被选取。

**说明：**

- 所有数字（包括 `target`）都是正整数。
- 解集不能包含重复的组合。 

**示例 1：**

```
输入：candidates = [2,3,6,7], target = 7,
所求解集为：
[
  [7],
  [2,2,3]
]
```

**示例 2：**

```
输入：candidates = [2,3,5], target = 8,
所求解集为：
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

 

**提示：**

- `1 <= candidates.length <= 30`
- `1 <= candidates[i] <= 200`
- `candidate` 中的每个元素都是独一无二的。
- `1 <= target <= 500`





```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> combinations = new ArrayList<>();
        backtracking(combinations, new ArrayList<Integer>(), 0, target, candidates);
        return combinations;
    }

    private void backtracking(List<List<Integer>> combinations, List<Integer> tempCombinations,
         int start, int target, int[] candidates) {

             if (target == 0) {
                 combinations.add(new ArrayList<>(tempCombinations));
                 return;
             }

             for (int i = start; i < candidates.length; i++) {
                 
                 if (candidates[i] <= target) {
                     tempCombinations.add(candidates[i]);
                     backtracking(combinations, tempCombinations, i, target - candidates[i], candidates);
                     tempCombinations.remove(tempCombinations.size() - 1);
                 }
             }
         }
}
```



2 2 2 当前值可能会重复选择





#### [40. 组合总和 II](https://leetcode-cn.com/problems/combination-sum-ii/)

难度中等483

给定一个数组 `candidates` 和一个目标数 `target` ，找出 `candidates` 中所有可以使数字和为 `target` 的组合。

`candidates` 中的每个数字在每个组合中只能使用一次。

**说明：**

- 所有数字（包括目标数）都是正整数。
- 解集不能包含重复的组合。 

**示例 1:**

```
输入: candidates = [10,1,2,7,6,1,5], target = 8,
所求解集为:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

**示例 2:**

```
输入: candidates = [2,5,2,1,2], target = 5,
所求解集为:
[
  [1,2,2],
  [5]
]
```





```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> combinations = new ArrayList<>();
        if (candidates == null || candidates.length == 0) {
            return combinations;
        }
        Arrays.sort(candidates);
        boolean[] hasVisited = new boolean[candidates.length];
        backtracking(combinations, new ArrayList<Integer>(), 0, target, hasVisited, candidates);
        return combinations;
        
    }

    private void backtracking(List<List<Integer>> combinations, List<Integer> tempCombination,
        int start, int target, boolean[] hasVisited, int[] candidates) {
            if (target == 0) {
                combinations.add(new ArrayList<>(tempCombination));
                return;
            }

            for (int i = start; i < candidates.length; i++) {
                if (i != 0 && candidates[i] == candidates[i - 1] && !hasVisited[i - 1]) {
                    continue;
                } 
                if (candidates[i] <= target) {
                    hasVisited[i] = true;
                    tempCombination.add(candidates[i]);
                    backtracking(combinations, tempCombination, i + 1, target -  candidates[i],
                        hasVisited, candidates);
                    hasVisited[i] = false;
                    tempCombination.remove(tempCombination.size() - 1);
                }
            }
        }
}
```



#### [216. 组合总和 III](https://leetcode-cn.com/problems/combination-sum-iii/)

难度中等255

找出所有相加之和为 ***n*** 的 ***k\*** 个数的组合***。\***组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

**说明：**

- 所有数字都是正整数。
- 解集不能包含重复的组合。 

**示例 1:**

```
输入: k = 3, n = 7
输出: [[1,2,4]]
```

**示例 2:**

```
输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
```



```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> combinations  = new ArrayList<>();
        backtracking(combinations, new ArrayList<Integer>(), 1, k, n);
        return combinations;
    }

    private void backtracking(List<List<Integer>> combinations, List<Integer> tempCombinations,
        int start, int k, int n) {
        
        if (k == 0 && n == 0) {
            combinations.add(new ArrayList<>(tempCombinations));
            return;
        }
        if (k == 0 || n == 0) {
            return;
        }

        for (int i = start; i <= 9; i++) {
            tempCombinations.add(i);
            backtracking(combinations, tempCombinations, i + 1,  k - 1, n - i);
            tempCombinations.remove(tempCombinations.size() - 1);
        }
    }
}
```



#### [78. 子集](https://leetcode-cn.com/problems/subsets/)

难度中等978

给你一个整数数组 `nums` ，数组中的元素 **互不相同** 。返回该数组所有可能的子集（幂集）。

解集 **不能** 包含重复的子集。你可以按 **任意顺序** 返回解集。

 

**示例 1：**

```
输入：nums = [1,2,3]
输出：[[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

**示例 2：**

```
输入：nums = [0]
输出：[[],[0]]
```

 

**提示：**

- `1 <= nums.length <= 10`
- `-10 <= nums[i] <= 10`
- `nums` 中的所有元素 **互不相同**



```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> subsets = new ArrayList<>();
        
        for (int i = 0; i <= nums.length; i++) {
            backtracking(subsets, new ArrayList<Integer>(), 0, i, nums);
        }
        
        return subsets;
    }

    private void backtracking(List<List<Integer>> subsets, List<Integer> tempSubsets,
        int start, int size, int[] nums) {

            if (tempSubsets.size() == size) {
                subsets.add(new ArrayList<>(tempSubsets));
                return;
            }

            for (int i = start; i < nums.length; i++) {
                tempSubsets.add(nums[i]);
                backtracking(subsets, tempSubsets, i + 1, size, nums);
                tempSubsets.remove(tempSubsets.size() - 1);
            }
            
        }
}
```





#### [90. 子集 II](https://leetcode-cn.com/problems/subsets-ii/)

难度中等378

给定一个可能包含重复元素的整数数组 ***nums***，返回该数组所有可能的子集（幂集）。

**说明：**解集不能包含重复的子集。

**示例:**

```
输入: [1,2,2]
输出:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```



需要先排序

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> subsets = new ArrayList<>();
        if (nums == null) {
            return subsets;
        }
        List<Integer> tempSubsets = new ArrayList<>();
        boolean[] hasVisited = new boolean[nums.length];
        for (int i = 0; i <= nums.length; i++) {
            backtracking(subsets, tempSubsets, 0, i, hasVisited, nums);
        }
        return subsets;
    }

    private void backtracking(List<List<Integer>> subsets, List<Integer> tempSubsets,
        int start, int size, boolean[] hasVisited,  int[] nums) {
            if (tempSubsets.size() == size) {
                subsets.add(new ArrayList<>(tempSubsets));
                return;
            }

            for (int i = start; i < nums.length; i++) {
                if (i != 0 && nums[i] == nums[i - 1] && !hasVisited[i - 1]) {
                    continue;
                }
                hasVisited[i] = true;
                tempSubsets.add(nums[i]);
                backtracking(subsets, tempSubsets, i + 1, size, hasVisited, nums);
                hasVisited[i] = false;
                tempSubsets.remove(tempSubsets.size() - 1);
            }
        }
}
```



#### [131. 分割回文串](https://leetcode-cn.com/problems/palindrome-partitioning/)

难度中等475

给定一个字符串 *s*，将 *s* 分割成一些子串，使每个子串都是回文串。

返回 *s* 所有可能的分割方案。

**示例:**

```
输入: "aab"
输出:
[
  ["aa","b"],
  ["a","a","b"]
]
```





```java
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> partitions = new ArrayList<>();
        backtracking(partitions, new ArrayList<String>(), s);
        return partitions;
    }

    private void backtracking(List<List<String>> partitions, List<String> tempPartitions,
        String s) {

            if (s.length() == 0) {
                partitions.add(new ArrayList<>(tempPartitions));
                return;
            }

            for (int i = 0; i < s.length(); i++) {
                if (isPalindrome(s, 0, i)) {
                    tempPartitions.add(s.substring(0, i + 1));
                    backtracking(partitions, tempPartitions, s.substring(i + 1));
                    tempPartitions.remove(tempPartitions.size() - 1);
                }
            }
        }

    private boolean isPalindrome(String str, int l, int r) {
        
        while (l < r) {
            if (str.charAt(l++) != str.charAt(r--)) {
                return false;
            }
        }
        return true;
    }
}
```





#### [37. 解数独](https://leetcode-cn.com/problems/sudoku-solver/)

难度困难744

编写一个程序，通过填充空格来解决数独问题。

一个数独的解法需**遵循如下规则**：

1. 数字 `1-9` 在每一行只能出现一次。
2. 数字 `1-9` 在每一列只能出现一次。
3. 数字 `1-9` 在每一个以粗实线分隔的 `3x3` 宫内只能出现一次。

空白格用 `'.'` 表示。

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

一个数独。

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png)

答案被标成红色。

**提示：**

- 给定的数独序列只包含数字 `1-9` 和字符 `'.'` 。
- 你可以假设给定的数独只有唯一解。
- 给定数独永远是 `9x9` 形式的。





```java
class Solution {

    private boolean[][] rowsUsed = new boolean[9][10];
    private boolean[][] colsUsed = new boolean[9][10];
    private boolean[][] cubesUsed = new boolean[9][10];
    private char[][] board;
    public void solveSudoku(char[][] board) {
        this.board = board;

        for (int i = 0; i < board.length; i++) {
            for (int j = 0; j < board[0].length; j++) {
                if (board[i][j] != '.') {
                    rowsUsed[i][board[i][j] - '0'] = true;
                    colsUsed[j][board[i][j] - '0'] = true;
                    cubesUsed[cubeNum(i, j)][board[i][j] - '0'] = true;
                }
            }
        }
        backtracking(0, 0);
    }

    private boolean backtracking(int row, int col) {
        while (row < 9 && board[row][col] != '.') {
            row = col == 8 ? row + 1 : row;
            col = col == 8 ? 0 : col + 1;
        }

        if (row == 9) {
            return true;
        }


        for (int i = 1; i <= 9; i++) {
            if (rowsUsed[row][i] || colsUsed[col][i] || cubesUsed[cubeNum(row, col)][i]) {
                continue;
            }
            rowsUsed[row][i] = true;
            colsUsed[col][i] = true;
            cubesUsed[cubeNum(row, col)][i] = true;
            board[row][col] = (char)(i + '0');
            if (backtracking(row, col)) {
                return true;
            }
            rowsUsed[row][i] = false;
            colsUsed[col][i] = false;
            cubesUsed[cubeNum(row, col)][i] = false;
            board[row][col] = '.';

       }
       return false;

        
    }

    private int cubeNum(int i, int j) {
        int row = i / 3;
        int col = j / 3;
        return row * 3 + col;
    }
}
```





### 贪心算法

*每次操作都是最优的，并且保证最后的结果时最优的*



#### [455. 分发饼干](https://leetcode-cn.com/problems/assign-cookies/)

难度简单299

假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。

对每个孩子 `i`，都有一个胃口值 `g[i]`，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 `j`，都有一个尺寸 `s[j]` 。如果 `s[j] >= g[i]`，我们可以将这个饼干 `j` 分配给孩子 `i` ，这个孩子会得到满足。你的目标是尽可能满足越多数量的孩子，并输出这个最大数值。

**示例 1:**

```
输入: g = [1,2,3], s = [1,1]
输出: 1
解释: 
你有三个孩子和两块小饼干，3个孩子的胃口值分别是：1,2,3。
虽然你有两块小饼干，由于他们的尺寸都是1，你只能让胃口值是1的孩子满足。
所以你应该输出1。
```

**示例 2:**

```
输入: g = [1,2], s = [1,2,3]
输出: 2
解释: 
你有两个孩子和三块小饼干，2个孩子的胃口值分别是1,2。
你拥有的饼干数量和尺寸都足以让所有孩子满足。
所以你应该输出2.
```

 

**提示：**

- `1 <= g.length <= 3 * 104`
- `0 <= s.length <= 3 * 104`
- `1 <= g[i], s[j] <= 231 - 1`







*小的饼干给小的同学，保证大的饼干不浪费*

证明：

​	现在把m饼干给朋友，现在m < n, n是最优解，那么最终剩下的饼干的大小一定比贪心算法大，所以贪心算法可以保证最优

gi 并不是每轮都增加所以使用while

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {

        if (g == null || s == null) {
            return 0;
        }
        Arrays.sort(g);
        Arrays.sort(s);
        int gi = 0;
        int si = 0;
        while (gi < g.length && si < s.length) {
            if (g[gi] <= s[si]) {
                gi++;
            }
            si++;
        }
        return gi;

    }
}
```





#### [435. 无重叠区间](https://leetcode-cn.com/problems/non-overlapping-intervals/)

难度中等346

给定一个区间的集合，找到需要移除区间的最小数量，使剩余区间互不重叠。

**注意:**

1. 可以认为区间的终点总是大于它的起点。
2. 区间 [1,2] 和 [2,3] 的边界相互“接触”，但没有相互重叠。

**示例 1:**

```
输入: [ [1,2], [2,3], [3,4], [1,3] ]

输出: 1

解释: 移除 [1,3] 后，剩下的区间没有重叠。
```

**示例 2:**

```
输入: [ [1,2], [1,2], [1,2] ]

输出: 2

解释: 你需要移除两个 [1,2] 来使剩下的区间没有重叠。
```



```
o1 - o2 :可能会产生Integer越界
```





*[1, 2] [2, 3]:认为不重叠*

*数组长度-不重叠长度*



```java
o1[i][1]:进行排序，保证小的数放在前面，给后面流的位置就大
```





```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {

        if (intervals == null || intervals.length == 0) {
            return 0;
        }

        Arrays.sort(intervals, Comparator.comparingInt(o -> o[1]));
        int cnt = 1;
        int end = intervals[0][1];
        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] < end) {
                continue;
            }
            end = intervals[i][1];
            ++cnt;
        }
        return intervals.length - cnt;
    }
}
```





```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        if (intervals == null || intervals.length == 0) {
            return 0;
        }
        Arrays.sort(intervals, (o1, o2) -> {
            return o1[1] < o2[1] ? -1 : (o1[1] == o2[1] ? 0 : 1); 
        });

        int cnt = 1;
        int end = intervals[0][1];
        for (int i = 1; i < intervals.length; i++) {
            if (intervals[i][0] < end) {
                continue;
            }
            cnt++;
            end = intervals[i][1];
        }
        return intervals.length - cnt;
    }
}
```





#### [452. 用最少数量的箭引爆气球](https://leetcode-cn.com/problems/minimum-number-of-arrows-to-burst-balloons/)

难度中等371

在二维空间中有许多球形的气球。对于每个气球，提供的输入是水平方向上，气球直径的开始和结束坐标。由于它是水平的，所以纵坐标并不重要，因此只要知道开始和结束的横坐标就足够了。开始坐标总是小于结束坐标。

一支弓箭可以沿着 x 轴从不同点完全垂直地射出。在坐标 x 处射出一支箭，若有一个气球的直径的开始和结束坐标为 `x``start`，`x``end`， 且满足  `xstart ≤ x ≤ x``end`，则该气球会被引爆。可以射出的弓箭的数量没有限制。 弓箭一旦被射出之后，可以无限地前进。我们想找到使得所有气球全部被引爆，所需的弓箭的最小数量。

给你一个数组 `points` ，其中 `points [i] = [xstart,xend]` ，返回引爆所有气球所必须射出的最小弓箭数。

**示例 1：**

```
输入：points = [[10,16],[2,8],[1,6],[7,12]]
输出：2
解释：对于该样例，x = 6 可以射爆 [2,8],[1,6] 两个气球，以及 x = 11 射爆另外两个气球
```

**示例 2：**

```
输入：points = [[1,2],[3,4],[5,6],[7,8]]
输出：4
```

**示例 3：**

```
输入：points = [[1,2],[2,3],[3,4],[4,5]]
输出：2
```

**示例 4：**

```
输入：points = [[1,2]]
输出：1
```

**示例 5：**

```
输入：points = [[2,3],[2,3]]
输出：1
```

 

**提示：**

- `0 <= points.length <= 104`
- `points[i].length == 2`
- `-231 <= xstart < xend <= 231 - 1`







和上一个题是类似的，都是求不重叠数组，只不过这个题

```
[0][1] 和[1][2]看作重叠
```







```java
class Solution {
    public int findMinArrowShots(int[][] points) {
        
        if (points == null || points.length == 0) {
            return 0;
        }

        Arrays.sort(points, Comparator.comparingInt(o -> o[1]));
        int cnt = 1;
        int end = points[0][1];
        for (int i = 1; i < points.length; i++) {
            if (points[i][0] <= end) {
                continue;
            }
            end = points[i][1];
            cnt++;
        }
        return cnt;
    }
}
```





#### [406. 根据身高重建队列](https://leetcode-cn.com/problems/queue-reconstruction-by-height/)

难度中等816

假设有打乱顺序的一群人站成一个队列，数组 `people` 表示队列中一些人的属性（不一定按顺序）。每个 `people[i] = [hi, ki]` 表示第 `i` 个人的身高为 `hi` ，前面 **正好** 有 `ki` 个身高大于或等于 `hi` 的人。

请你重新构造并返回输入数组 `people` 所表示的队列。返回的队列应该格式化为数组 `queue` ，其中 `queue[j] = [hj, kj]` 是队列中第 `j` 个人的属性（`queue[0]` 是排在队列前面的人）。

 



**示例 1：**

```
输入：people = [[7,0],[4,4],[7,1],[5,0],[6,1],[5,2]]
输出：[[5,0],[7,0],[5,2],[6,1],[4,4],[7,1]]
解释：
编号为 0 的人身高为 5 ，没有身高更高或者相同的人排在他前面。
编号为 1 的人身高为 7 ，没有身高更高或者相同的人排在他前面。
编号为 2 的人身高为 5 ，有 2 个身高更高或者相同的人排在他前面，即编号为 0 和 1 的人。
编号为 3 的人身高为 6 ，有 1 个身高更高或者相同的人排在他前面，即编号为 1 的人。
编号为 4 的人身高为 4 ，有 4 个身高更高或者相同的人排在他前面，即编号为 0、1、2、3 的人。
编号为 5 的人身高为 7 ，有 1 个身高更高或者相同的人排在他前面，即编号为 1 的人。
因此 [[5,0],[7,0],[5,2],[6,1],[4,4],[7,1]] 是重新构造后的队列。
```



对题目给定的数组插入到指定的位置，





身高降序，身高相等个数升序，

如果身高低的先插入，身高高的后插入，会改变之前的位置

5， 0     10， 0

5，0 会变为 5，1



```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {

        if (people == null || people.length == 0 || people[0].length == 0) {
            return new int[0][0];
        }

        Arrays.sort(people, (o1, o2) -> o1[0] == o2[0] ? o1[1] - o2[1] : o2[0] - o1[0]);
        List<int[]> queue = new ArrayList<>();
        for (int[] p : people) {
            queue.add(p[1], p);
        }
        return queue.toArray(new int[queue.size()][]);
    }
}
```





#### [121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

难度简单1531

给定一个数组 `prices` ，它的第 `i` 个元素 `prices[i]` 表示一支给定股票第 `i` 天的价格。

你只能选择 **某一天** 买入这只股票，并选择在 **未来的某一个不同的日子** 卖出该股票。设计一个算法来计算你所能获取的最大利润。

返回你可以从这笔交易中获取的最大利润。如果你不能获取任何利润，返回 `0` 。

 

**示例 1：**

```
输入：[7,1,5,3,6,4]
输出：5
解释：在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
```



最低价格买入，最高迈出



```java
class Solution {
    
    public int maxProfit(int[] prices) {
        int minPrice = Integer.MAX_VALUE;
        int maxProfit = 0;
        
        for(int price : prices) {
            if (price < minPrice) {
                minPrice = price;
            } else {
                maxProfit = Math.max(maxProfit, price - minPrice);
            }
        }
        return maxProfit;
    }
}
```









#### [122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

难度简单1155

给定一个数组，它的第 *i* 个元素是一支给定股票第 *i* 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

**注意：**你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

 

**示例 1:**

```
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
```

**示例 2:**

```
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```

**示例 3:**

```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```





```java
class Solution {
    public int maxProfit(int[] prices) {

        if (prices == null || prices.length < 2) {
            return 0;
        }

        int len = prices.length;
        int[][] dp = new int[len][2];
        dp[0][1] = -prices[0];

        for (int i = 1; i < len; i++) {
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] + prices[i]);
            dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] - prices[i]);
        }
        return dp[len - 1][0];

    }
}
```







#### [605. 种花问题](https://leetcode-cn.com/problems/can-place-flowers/)

难度简单322

假设有一个很长的花坛，一部分地块种植了花，另一部分却没有。可是，花不能种植在相邻的地块上，它们会争夺水源，两者都会死去。

给你一个整数数组 `flowerbed` 表示花坛，由若干 `0` 和 `1` 组成，其中 `0` 表示没种植花，`1` 表示种植了花。另有一个数 `n` ，能否在不打破种植规则的情况下种入 `n` 朵花？能则返回 `true` ，不能则返回 `false`。

 

**示例 1：**

```
输入：flowerbed = [1,0,0,0,1], n = 1
输出：true
```

**示例 2：**

```
输入：flowerbed = [1,0,0,0,1], n = 2
输出：false
```

 

**提示：**

- `1 <= flowerbed.length <= 2 * 104`
- `flowerbed[i]` 为 `0` 或 `1`
- `flowerbed` 中不存在相邻的两朵花
- `0 <= n <= flowerbed.length`





```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {

        if (flowerbed == null) {
            return true;
        }

        int cnt = 0;
        int len = flowerbed.length;
        for (int i = 0; i < len; i++) {
            if (flowerbed[i] == 1) {
                continue;
            }

            int pre = i == 0 ? 0 : flowerbed[i - 1];
            int next = i == len - 1 ? 0 : flowerbed[i + 1];
            if (pre == 0 && next == 0) {
                cnt++;
                flowerbed[i] = 1;
            }
        }
        return cnt >= n;

    }
}
```









### DP



#### [70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

难度简单1457

假设你正在爬楼梯。需要 *n* 阶你才能到达楼顶。

每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？

**注意：**给定 *n* 是一个正整数。

**示例 1：**

```
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶
```

**示例 2：**

```
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```





```java
class Solution {
    public int climbStairs(int n) {

        if (n <= 1) {
            return 1;
        }
        int[] dp = new int[n];
        dp[0] = 1;
        dp[1] = 2;
        for (int i = 2; i < n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n - 1];

    }
}
```





```java
class Solution {
    public int climbStairs(int n) {

        if (n <= 1) {
            return 1;
        }
        int pre2 = 1;
        int pre1 = 2;
        for (int i = 2; i < n; i++) {
            int cur = pre2 + pre1;
            pre2 = pre1;
            pre1 = cur;
        }
        return pre1;

    }
}
```



#### [198. 打家劫舍](https://leetcode-cn.com/problems/house-robber/)

难度中等1270

你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，**如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警**。

给定一个代表每个房屋存放金额的非负整数数组，计算你 **不触动警报装置的情况下** ，一夜之内能够偷窃到的最高金额。

 

**示例 1：**

```
输入：[1,2,3,1]
输出：4
解释：偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
     偷窃到的最高金额 = 1 + 3 = 4 。
```

**示例 2：**

```
输入：[2,7,9,3,1]
输出：12
解释：偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。
     偷窃到的最高金额 = 2 + 9 + 1 = 12 。
```

 

**提示：**

- `0 <= nums.length <= 100`
- `0 <= nums[i] <= 400`



```java
class Solution {
    public int rob(int[] nums) {

        int pre2 = 0;
        int pre1 = 0;
        for (int i = 0; i < nums.length; i++) {
            int cur = Math.max(pre2 + nums[i], pre1);
            pre2 = pre1;
            pre1 = cur;
        }
        return pre1;
    }
}
```





#### [213. 打家劫舍 II](https://leetcode-cn.com/problems/house-robber-ii/)

难度中等461

你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都 **围成一圈** ，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，**如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警** 。

给定一个代表每个房屋存放金额的非负整数数组，计算你 **在不触动警报装置的情况下** ，能够偷窃到的最高金额。

 

**示例 1：**

```
输入：nums = [2,3,2]
输出：3
解释：你不能先偷窃 1 号房屋（金额 = 2），然后偷窃 3 号房屋（金额 = 2）, 因为他们是相邻的。
```

**示例 2：**

```
输入：nums = [1,2,3,1]
输出：4
解释：你可以先偷窃 1 号房屋（金额 = 1），然后偷窃 3 号房屋（金额 = 3）。
     偷窃到的最高金额 = 1 + 3 = 4 。
```

**示例 3：**

```
输入：nums = [0]
输出：0
```

 

**提示：**

- `1 <= nums.length <= 100`
- `0 <= nums[i] <= 1000`



```java
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }

        if (nums.length == 1) {
            return nums[0];
        }

        return Math.max(rob(nums, 0, nums.length - 2), rob(nums, 1, nums.length - 1));


    }

    public int rob(int[] nums, int f, int l) {

        int pre2 = 0;
        int pre1 = 0;
        for (int i = f; i <= l; i++) {
            int cur = Math.max(pre2 + nums[i], pre1);
            pre2 = pre1;
            pre1 = cur;
        }
        return pre1;
    }
}
```



#### 4.信件错排

题目描述：有n个信和信封，求他有多少种错误的方式

定义一个数组 dp 存储错误方式数量，dp[i] 表示前 i 个信和信封的错误方式数量。假设第 i 个信装到第 j 个信封里面，而第 j 个信装到第 k 个信封里面。根据 i 和 k 是否相等，有两种情况：

- i==k，此时i的选择i-1种，(i - 1) * dp[i - 2],因为i 和 j已经忽略，所以剩下i-2
- i != k，(i-1) * dp[i-1]



```java
public class Message {

    public static int getMessageSum(int n) {

        if (n <= 1) {
            return 0;
        }
        int pre2 = 0;
        int pre1 = 1;

        for (int i = 3; i <= n; i++) {
            int cur = (i - 1) * pre2 + (i - 1) * pre1;
            pre2 = pre1;
            pre1 = cur;

        }
        return pre1;
    }

    public static void main(String[] args) {

        System.out.println(getMessageSum(5));

    }

}

```

#### 母牛生产

题目描述：假设农场中成熟的母牛每年都会生 1 头小母牛，并且永远不会死。第一年有 1 只小母牛，从第二年开始，母牛开始生小母牛。每只小母牛 3 年之后成熟又可以生小母牛。给定整数 N，求 N 年后牛的数量。



```java
// dp[i - 1] :上一年牛的数量  dp[i - 3]成熟母牛的数量
dp[i] = dp[i - 1] + dp[i - 3]; 
```



#### **>>矩阵路径>>**



#### [64. 最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)

难度中等781

给定一个包含非负整数的 `*m* x *n*` 网格 `grid` ，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

**说明：**每次只能向下或者向右移动一步。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg)

```
输入：grid = [[1,3,1],[1,5,1],[4,2,1]]
输出：7
解释：因为路径 1→3→1→1→1 的总和最小。
```

**示例 2：**

```
输入：grid = [[1,2,3],[4,5,6]]
输出：12
```

 

**提示：**

- `m == grid.length`
- `n == grid[i].length`
- `1 <= m, n <= 200`
- `0 <= grid[i][j] <= 100`





**不会改变该列值3->3 和4没关系**

和最小



```java
class Solution {
    public int minPathSum(int[][] grid) {
        
        if(grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }
        int m = grid.length;
        int n = grid[0].length;
        int[] dp = new int[n];
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (j == 0) {
                    dp[j] = dp[j];
                } else if (i == 0) {
                    dp[j] = dp[j - 1];
                } else {
                    dp[j] = Math.min(dp[j], dp[j - 1]);
                }
                dp[j] += grid[i][j];
            }
        }
        return dp[n - 1];
    }
}
```





#### [62. 不同路径](https://leetcode-cn.com/problems/unique-paths/)

难度中等876

一个机器人位于一个 `m x n` 网格的左上角 （起始点在下图中标记为 “Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为 “Finish” ）。

问总共有多少条不同的路径？

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2018/10/22/robot_maze.png)

```
输入：m = 3, n = 7
输出：28
```

**示例 2：**

```
输入：m = 3, n = 2
输出：3
解释：
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向下 -> 向下
2. 向下 -> 向下 -> 向右
3. 向下 -> 向右 -> 向下
```

**示例 3：**

```
输入：m = 7, n = 3
输出：28
```

**示例 4：**

```
输入：m = 3, n = 3
输出：6
```

 

**提示：**

- `1 <= m, n <= 100`
- 题目数据保证答案小于等于 `2 * 109`



```java
class Solution {
    public int uniquePaths(int m, int n) {
        int[] dp = new int[n];
        Arrays.fill(dp, 1);
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[j] = dp[j] + dp[j - 1];
            }
        }
        return dp[n - 1];
    }
}
```









#### [416. 分割等和子集](https://leetcode-cn.com/problems/partition-equal-subset-sum/)

难度中等695

给定一个**只包含正整数**的**非空**数组。是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

**注意:**

1. 每个数组中的元素不会超过 100
2. 数组的大小不会超过 200

**示例 1:**

```
输入: [1, 5, 11, 5]

输出: true

解释: 数组可以分割成 [1, 5, 5] 和 [11].
```

 

**示例 2:**

```
输入: [1, 2, 3, 5]

输出: false

解释: 数组不能分割成两个元素和相等的子集.
```





```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = computeArraySum(nums);
        if (sum % 2 == 1) {
            return false;
        }
        int W = sum / 2;
        boolean[] dp = new boolean[W + 1];
        dp[0] = true;
        for (int num : nums) {
            for (int j = W; j >= num; j--){
                dp[j] = dp[j] || dp[j - num];
            }
        }
        return dp[W];

    }

    private int computeArraySum(int[] nums) {
        int sum = 0;
        for (int num: nums) {
            sum += num;
        }
        return sum;
    }
    
}
```





#### [494. 目标和](https://leetcode-cn.com/problems/target-sum/)

难度中等586

给定一个非负整数数组，a1, a2, ..., an, 和一个目标数，S。现在你有两个符号 `+` 和 `-`。对于数组中的任意一个整数，你都可以从 `+` 或 `-`中选择一个符号添加在前面。

返回可以使最终数组和为目标数 S 的所有添加符号的方法数。

 

**示例：**

```
输入：nums: [1, 1, 1, 1, 1], S: 3
输出：5
解释：

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

一共有5种方法让最终目标和为3。
```

 

**提示：**

- 数组非空，且长度不会超过 20 。
- 初始的数组的和不会超过 1000 。
- 保证返回的最终结果能被 32 位整数存下。



和小于目标值

```java
class Solution {
    public int findTargetSumWays(int[] nums, int S) {
        int sum = computeArraySum(nums);
        if (sum < S || (sum + S) % 2 == 1) {
            return 0;
        }
        int W = (sum + S) / 2;
        int[] dp = new int[W + 1];
        dp[0] = 1;
        for (int num : nums) {
            for (int i = W; i >= num; i--) {
                dp[i] = dp[i] + dp[i - num];
            }
        }
        return dp[W];
    }

    private int computeArraySum(int[] nums) {
        int sum = 0;
        for (int num : nums) {
            sum += num;
        }
        return sum;
    }
}
```



#### [474. 一和零](https://leetcode-cn.com/problems/ones-and-zeroes/)

难度中等356

给你一个二进制字符串数组 `strs` 和两个整数 `m` 和 `n` 。

请你找出并返回 `strs` 的最大子集的大小，该子集中 **最多** 有 `m` 个 `0` 和 `n` 个 `1` 。

如果 `x` 的所有元素也是 `y` 的元素，集合 `x` 是集合 `y` 的 **子集** 。

 

**示例 1：**

```
输入：strs = ["10", "0001", "111001", "1", "0"], m = 5, n = 3
输出：4
解释：最多有 5 个 0 和 3 个 1 的最大子集是 {"10","0001","1","0"} ，因此答案是 4 。
其他满足题意但较小的子集包括 {"0001","1"} 和 {"10","1","0"} 。{"111001"} 不满足题意，因为它含 4 个 1 ，大于 n 的值 3 。
```

**示例 2：**

```
输入：strs = ["10", "0", "1"], m = 1, n = 1
输出：2
解释：最大的子集是 {"0", "1"} ，所以答案是 2 。
```

 

**提示：**

- `1 <= strs.length <= 600`
- `1 <= strs[i].length <= 100`
- `strs[i]` 仅由 `'0'` 和 `'1'` 组成
- `1 <= m, n <= 100`





```java
class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        if (strs == null || strs.length == 0) {
            return 0;
        }
        int[][] dp = new int[m + 1][n + 1];
        for (String str : strs) {
            int zeros = 0;
            int ones = 0;
            for (char ch : str.toCharArray()) {
                if (ch == '0') {
                    zeros++;
                } else {
                    ones++;
                }
            }

            for (int i = m; i >= zeros; i--) {
                for (int j = n; j >= ones; j--) {
                    dp[i][j] = Math.max(dp[i][j], dp[i - zeros][j - ones] + 1);
                }
            }
        }
        return dp[m][n];
    }
}
```



#### [322. 零钱兑换](https://leetcode-cn.com/problems/coin-change/)

难度中等1122

给定不同面额的硬币 `coins` 和一个总金额 `amount`。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 `-1`。

你可以认为每种硬币的数量是无限的。

 

**示例 1：**

```
输入：coins = [1, 2, 5], amount = 11
输出：3 
解释：11 = 5 + 5 + 1
```

**示例 2：**

```
输入：coins = [2], amount = 3
输出：-1
```





```java
class Solution {
    public int coinChange(int[] coins, int amount) {
        if (coins == null || amount == 0) {
            return 0;
        }
        int[] dp = new int[amount + 1];
        
        for(int coin : coins) {
            
            for (int i = coin; i <= amount; i++) {
                if (i == coin) {
                    dp[i] = 1;
                } else if (dp[i] == 0 && dp[i - coin] != 0) {
                    dp[i] = dp[i - coin] + 1;
                } else if (dp[i - coin] != 0) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }
        return dp[amount] == 0 ? -1 : dp[amount];
    }
}
```



#### [518. 零钱兑换 II](https://leetcode-cn.com/problems/coin-change-2/)

难度中等335

给定不同面额的硬币和一个总金额。写出函数来计算可以凑成总金额的硬币组合数。假设每一种面额的硬币有无限个。 

 



**示例 1:**

```
输入: amount = 5, coins = [1, 2, 5]
输出: 4
解释: 有四种方式可以凑成总金额:
5=5
5=2+2+1
5=2+1+1+1
5=1+1+1+1+1
```

**示例 2:**

```
输入: amount = 3, coins = [2]
输出: 0
解释: 只用面额2的硬币不能凑成总金额3。
```

**示例 3:**

```
输入: amount = 10, coins = [10] 
输出: 1
```

 

**注意****:**

你可以假设：

- 0 <= amount (总金额) <= 5000
- 1 <= coin (硬币面额) <= 5000
- 硬币种类不超过 500 种
- 结果符合 32 位符号整数



```java
class Solution {
    public int change(int amount, int[] coins) {
        if (amount == 0) {
            return 1;
        }
        int[] dp = new int[amount + 1];
        dp[0] = 1;
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] = dp[i] + dp[i - coin];
            }
        }
        return dp[amount]; 
    }
}
```



#### [139. 单词拆分](https://leetcode-cn.com/problems/word-break/)

难度中等875

给定一个**非空**字符串 *s* 和一个包含**非空**单词的列表 *wordDict*，判定 *s* 是否可以被空格拆分为一个或多个在字典中出现的单词。

**说明：**

- 拆分时可以重复使用字典中的单词。
- 你可以假设字典中没有重复的单词。

**示例 1：**

```
输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。
```

**示例 2：**

```
输入: s = "applepenapple", wordDict = ["apple", "pen"]
输出: true
解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。
     注意你可以重复使用字典中的单词。
```

**示例 3：**

```
输入: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
输出: false
```



```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        int len = s.length();
        boolean[] dp = new boolean[len + 1];
        dp[0] = true;
        for (int i = 1; i <= len; i++) {
            for (String word : wordDict) {
                int wordLen = word.length();
                if (i >= wordLen && word.equals(s.substring(i - wordLen, i))) {
                    dp[i] = dp[i] || dp[i - wordLen];
                }
            }
        }
        return dp[len];

  }
}
```









### 链表



#### [160. 相交链表](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

难度简单1023

编写一个程序，找到两个单链表相交的起始节点。

如下面的两个链表**：**

[![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_statement.png)

在节点 c1 开始相交。

 

**示例 1：**

[![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/160_example_1.png)](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)

```
输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个链表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
```





```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode l1 = headA;
        ListNode l2 = headB;

    while(l1 != l2) {
            l1 = (l1 == null) ? headB : l1.next;
            l2 = (l2 == null) ? headA : l2.next;
        }
        return l1;
    }
}
```

#### [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

难度简单1566

反转一个单链表。

**示例:**

```
输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

反转

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode curr = head;
        ListNode pre = null;
        while (curr != null) {
            ListNode next = curr.next;
            curr.next = pre;
            pre = curr;
            curr = next;
        }
        return pre;
       
    }
}
```



递归

```java
 public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode res = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return res;
    }
```

#### [21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

难度简单1589

将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

```
输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]
```





```java
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        if (l1.val < l2.val) {
            l1.next = mergeTwoLists(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeTwoLists(l1, l2.next);
            return l2;
        }
    }
}
```





#### [83. 删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

难度简单488

给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

**示例 1:**

```
输入: 1->1->2
输出: 1->2
```

**示例 2:**

```
输入: 1->1->2->3->3
输出: 1->2->3
```



递归

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        head.next = deleteDuplicates(head.next);
        return head.val == head.next.val ? head.next : head;
    }
}
```





```java

class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        Set<Integer> set = new HashSet<>();
        ListNode pre = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode next = curr.next;
            if (!set.add(curr.val)) {
                pre.next = next;
                
            } else {
                pre = curr;
            }            
            curr = next;
        }
         return head;
    }
}
```



我自己的版本



```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        Set<Integer> set = new HashSet<>();
        ListNode cur = head;
        ListNode pre = null;
        while (cur != null) {
            if (set.contains(cur.val)) {
                pre.next = cur.next;
                cur = pre.next;
            } else {
                set.add(cur.val);
                pre = cur;
                cur = cur.next;
                
            }
        }
        return head;
    }
}
```





#### [19. 删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)

难度中等1264

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

**进阶：**你能尝试使用一趟扫描实现吗？

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

**示例 2：**

```
输入：head = [1], n = 1
输出：[]
```

**示例 3：**

```
输入：head = [1,2], n = 1
输出：[1]
```





```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        
        ListNode fast = head;
        while (n-- > 0) {
            if (fast == null) {
                return head;
            }
            fast = fast.next;
            
        }
        if (fast == null) {
            return head.next;
        }
        ListNode slow = head;
        while (fast.next != null) {
            fast = fast.next;
            slow = slow.next;
        }
        slow.next = slow.next.next;
        return head;
    }
}
```

#### [24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

难度中等848

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

**你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/10/03/swap_ex1.jpg)

```
输入：head = [1,2,3,4]
输出：[2,1,4,3]
```



```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode node = new ListNode(-1);
        node.next = head;
        ListNode pre = node;
        while (pre.next != null && pre.next.next != null) {
            ListNode l1 = pre.next;
            ListNode l2 = pre.next.next;
            ListNode next = l2.next;
            l1.next = next;
            l2.next = l1;
            pre.next = l2;

            pre = l1;
        }
        return node.next;
    }
}
```

#### [445. 两数相加 II](https://leetcode-cn.com/problems/add-two-numbers-ii/)

难度中等350

给你两个 **非空** 链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储一位数字。将这两数相加会返回一个新的链表。

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

 

**进阶：**

如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

 

**示例：**

```
输入：(7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 8 -> 0 -> 7
```



```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> stack1 = buildStack(l1);
        Stack<Integer> stack2 = buildStack(l2);
        int carry = 0;
        ListNode head = new ListNode(-1);
        while (!stack1.isEmpty() || !stack2.isEmpty() || carry != 0) {
            int num1 = stack1.isEmpty() ? 0 : stack1.pop();
            int num2 = stack2.isEmpty() ? 0 : stack2.pop();
            int sum = num1 + num2 + carry;
            ListNode node = new ListNode(sum % 10);
            node.next = head.next;
            head.next = node;
            carry = sum / 10;
        }
        return head.next;
    }


    public Stack<Integer> buildStack(ListNode node) {
        Stack<Integer> stack = new Stack<>();
        while (node != null) {
            stack.push(node.val);
            node = node.next;
        }
        return stack;
    }
}
```

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        l1 = reverseList(l1);
        l2 = reverseList(l2);
        ListNode head = new ListNode(-1);
        int carry = 0;
        int num1 = 0;
        int num2 = 0;
        while (l1 != null || l2 != null || carry != 0) {
           
            if (l1 != null) {
                num1 = l1.val;
                l1 = l1.next;
            } else {
                num1 = 0;
            }
            if (l2 != null) {
                num2 = l2.val;
                l2 = l2.next;
            } else {
                num2 = 0;
            }
            int sum = num1 + num2 + carry;
            ListNode node = new ListNode(sum % 10);
            node.next = head.next;
            head.next = node;
            carry = sum / 10;
        }
        return head.next;
    }

    public ListNode reverseList(ListNode node) {
        ListNode curr = node;
        ListNode pre = null;
        while (curr != null) {
            ListNode next = curr.next;
            curr.next = pre; // 因为会被破坏所以
            pre = curr;
            curr = next;
        }
        return pre;
    }
}
```



#### [234. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

难度简单891

请判断一个链表是否为回文链表。

**示例 1:**

```
输入: 1->2
输出: false
```





```java
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null || head.next == null) {
            return true;
        }
        ListNode slow = head;
        ListNode fast = head.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        if (fast != null) {
            slow = slow.next;
        }
        cut(head, slow);
        return isEqual(head, reverse(slow));
    }

    public void cut(ListNode node1, ListNode node2) {
        while (node1.next != node2) { // node1.next != node2
            node1 = node1.next;
        }
        node1.next = null;
    }

    public ListNode reverse(ListNode head) {
        
        ListNode pre = null;
        while (head != null) {
            ListNode next = head.next;
            head.next = pre;
            pre = head;
            head = next;
        }
        return pre;
    }

    public boolean isEqual(ListNode node1, ListNode node2) {
        
        while (node1 != null && node2 != null) {
            if (node1.val != node2.val) {
                return false;
            }
            node1 = node1.next;
            node2 = node2.next;
        }
        return true;
    }


}
```



递归

```java
class Solution {
    ListNode frontPointer = null;
    public boolean isPalindrome(ListNode head) {
        frontPointer = head;
        return recursivelyCheck(head);
    }

    private boolean recursivelyCheck(ListNode node) {
        if (node != null) {
            if(!recursivelyCheck(node.next)) {
                return false;
            }
            if (node.val == frontPointer.val) {
                frontPointer = frontPointer.next;
                return true;
            }
            return false;
        }
        return true;
    }
}
```





#### [725. 分隔链表](https://leetcode-cn.com/problems/split-linked-list-in-parts/)

难度中等124

给定一个头结点为 `root` 的链表, 编写一个函数以将链表分隔为 `k` 个连续的部分。

每部分的长度应该尽可能的相等: 任意两部分的长度差距不能超过 1，也就是说可能有些部分为 null。

这k个部分应该按照在链表中出现的顺序进行输出，并且排在前面的部分的长度应该大于或等于后面的长度。

返回一个符合上述规则的链表的列表。

举例： 1->2->3->4, k = 5 // 5 结果 [ [1], [2], [3], [4], null ]

**示例 1：**

```
输入: 
root = [1, 2, 3], k = 5
输出: [[1],[2],[3],[],[]]
解释:
输入输出各部分都应该是链表，而不是数组。
例如, 输入的结点 root 的 val= 1, root.next.val = 2, \root.next.next.val = 3, 且 root.next.next.next = null。
第一个输出 output[0] 是 output[0].val = 1, output[0].next = null。
最后一个元素 output[4] 为 null, 它代表了最后一个部分为空链表。
```

**示例 2：**

```
输入: 
root = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], k = 3
输出: [[1, 2, 3, 4], [5, 6, 7], [8, 9, 10]]
解释:
输入被分成了几个连续的部分，并且每部分的长度相差不超过1.前面部分的长度大于等于后面部分的长度。
```

 

**提示:**

- `root` 的长度范围： `[0, 1000]`.
- 输入的每个节点的大小范围：`[0, 999]`.
- `k` 的取值范围： `[1, 50]`.

 



```java
class Solution {
    public ListNode[] splitListToParts(ListNode root, int k) {
        ListNode[] res = new ListNode[k];
        ListNode cur = root;
        int N = 0;
        while (cur != null) { // 刚开始这里写成root导致
            N++;
            cur = cur.next;
        }
        int mod = N % k;
        int size = N / k;
        cur = root;
        for (int i = 0; i < k && cur != null; i++) {
            res[i] = cur;
            int curSize = size + (mod-- > 0 ? 1 : 0);
            for (int j = 0; j < curSize - 1; j++) {
                cur = cur.next;
            }
            ListNode next = cur.next;
            cur.next = null;
            cur = next;
        }
        return res;
    }
}
```



















#### [328. 奇偶链表](https://leetcode-cn.com/problems/odd-even-linked-list/)

难度中等394

给定一个单链表，把所有的奇数节点和偶数节点分别排在一起。请注意，这里的奇数节点和偶数节点指的是节点编号的奇偶性，而不是节点的值的奇偶性。

请尝试使用原地算法完成。你的算法的空间复杂度应为 O(1)，时间复杂度应为 O(nodes)，nodes 为节点总数。

**示例 1:**

```
输入: 1->2->3->4->5->NULL
输出: 1->3->5->2->4->NULL
```

**示例 2:**

```
输入: 2->1->3->5->6->4->7->NULL 
输出: 2->3->6->7->1->5->4->NULL
```

**说明:**

- 应当保持奇数节点和偶数节点的相对顺序。
- 链表的第一个节点视为奇数节点，第二个节点视为偶数节点，以此类推。





```java
class Solution {
    public ListNode oddEvenList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode odd = head;
        ListNode even = head.next;
        ListNode evenHead = even;
        while (even != null && even.next != null) {
            odd.next = odd.next.next;
            odd = odd.next;
            even.next = even.next.next;
            even = even.next;
        }
        odd.next = evenHead;
        return head;
    }
}
```





### end