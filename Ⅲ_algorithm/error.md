

```java
Math.random() // [0,1)
```






```java
int i = (int)9.9; // 9

```



```java
int[][] 少写了一个[]
```



**!=O**

```java
class Solution {
    int m;
    int n;
    int[][] direction = new int[][]{{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    public void solve(char[][] board) {
        if (board == null || board.length == 0 || board[0].length == 0) {
            return;
        }

        m = board.length;
        n = board[0].length;
        for (int i = 0; i < m; i++) {
            dfs(board, i, 0);
            dfs(board, i, n - 1);
        }
        for (int j = 0; j < n; j++) {
            dfs(board, 0, j);
            dfs(board, m - 1, j);
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

    private void dfs(char[][] board, int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >= n || board[i][j] != 'O') {
            return;
        }
        board[i][j] = 'T';
        for (int[] d : direction) {
            dfs(board, i + d[0], j + d[1]);
        }
    }
}
```

太平洋大西洋问题

四个方向：即使不可行之后会遍历

```java
class Solution {
    int m;
    int n;
    int[][] direction = new int[][]{{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    public List<List<Integer>> pacificAtlantic(int[][] matrix) {
        List<List<Integer>> res = new ArrayList<>();
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return res;
        }

        m = matrix.length;
        n = matrix[0].length;
        boolean[][] canReachP = new boolean[m][n];
        boolean[][] canReachA = new boolean[m][n];
        for (int i = 0; i < m; i++) {
            dfs(matrix, i, 0, canReachP);
            dfs(matrix, i, n - 1, canReachA);
        }
        for (int i = 0; i < n; i++) {
            dfs(matrix, 0, i, canReachP);
            dfs(matrix, m - 1, i, canReachA);
        }
        
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (canReachP[i][j] && canReachA[i][j]) {
                    List<Integer> tempRes = new ArrayList<>();
                    tempRes.add(i);
                    tempRes.add(j);
                    res.add(tempRes);
                }
            }
        }
        return res;

    }

    private void dfs(int[][] matrix, int i, int j, boolean[][] canReach) {
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
            dfs(matrix, nextR, nextC, canReach);
        }
    }
}
```





平方根

res = mid mid mid mid

```java
class Solution {
    public int mySqrt(int x) {
        if (x <= 0) {
            return 0;
        }
        int l = 1;
        int r = x;
        int res = Integer.MIN_VALUE;
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (mid > x / mid) {
                r = mid - 1;
            } else {
               l = mid + 1;
               res = mid;
            }
        }
        return res == Integer.MIN_VALUE ? - 1 : res;
    }
}
```



```java
LinkedList基本操作
```







```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        // 考虑 []0  ->
        if (nums == null || nums.length == 0 || nums.length < k) {
            return new int[]{};
        }
        int n = nums.length;
        int[] res = new int[n - k + 1];
        LinkedList<Integer> list = new LinkedList<>();

        for (int i = 1 - k, j = 0; j < n; i++, j++) {
            if (i > 0 && nums[i - 1] == list.peekFirst()) {
                list.removeFirst();
            }

            while (!list.isEmpty() && list.peekLast() < nums[j]) {
                list.removeLast();
            }
            list.addLast(nums[j]);
            
            if (i >= 0) {
                res[i] = list.peekFirst();
            }
        }
        return res;
    }
}
```





小顶堆大顶堆

res没定义

add :double 变量

```java
class Solution {
    public double[] medianSlidingWindow(int[] nums, int k) {

        if (nums == null || nums.length == 0 || nums.length < k) {
            return new double[]{};
        }
        
        PriorityQueue<Double> min = new PriorityQueue<>();
        PriorityQueue<Double> max = new PriorityQueue<>((o1, o2) -> {
            return o2.compareTo(o1);
        });
        int n = nums.length;
        double[] res = new double[n - k + 1];
        for (int i = 1 - k, j = 0; j < n; i++, j++) {
            if (i > 0) {
                remove(min, max, nums[i - 1]);
            }

            add(min, max, nums[j]);

            if (i >= 0) {
                if (min.size() == max.size()) {
                    res[i] = (min.peek() + max.peek()) * 0.5;
                } else {
                    res[i] = max.peek();
                }
            }
           
        }
         return res;
    }

    public void add(PriorityQueue<Double> min, PriorityQueue<Double> max, double num) {
        max.offer(num);
        min.offer(max.poll());
        if (max.size() < min.size()) {
            max.offer(min.poll());
        }
    }

    public void remove(PriorityQueue<Double> min, PriorityQueue<Double> max, double num) {
        if (num > max.peek()) {
            min.remove(num);
        } else {
            max.remove(num);
        }
    }
}
```





最长 while

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> set = new HashSet<>();
        int l = 0;
        int r = 0;
        int maxLen = 0;
        for (char ch : s.toCharArray()) {
            while (!set.add(ch)) {
                set.remove(s.charAt(l++));
            }
            r++;
            maxLen = Math.max(maxLen, r - l);
        } 
        return maxLen;
    }
}
```



超过一半的数字



count += (num == x ? 1 : 0); 

写成 count += (num == x ? 1 : -1); 

```java

class Solution {
    public int majorityElement(int[] nums) {
        int vote = 0;
        int x = 0;
        for(int num : nums) {
            if (vote == 0) {
                vote = 1;
                x = num;
            } else {
                vote += (x == num ? 1 : -1);
            }
        }
        int count = 0;
        for (int num : nums) {
            count += (num == x ? 1 : 0); 
        }
        return count > nums.length / 2 ? x : -1;
    }
}
```

== 写成=

int area  写成 area



```java

class Solution {
    int m;
    int n;
    int[][] direction = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};
    public int maxAreaOfIsland(int[][] grid) {
        if (grid == null || grid.length == 0 || grid[0].length == 0) {
            return 0;
        }

        int maxArea = 0;
        m = grid.length;
        n = grid[0].length;

        for(int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                maxArea = Math.max(maxArea, dfs(grid, i, j));
            }
        }
        return maxArea;
    }

    private int dfs(int[][] grid, int i, int j) {
        if (i < 0 || i >= m || j < 0 || j >= n || grid[i][j] == 0) {
            return 0;
        }

        grid[i][j] = 0;
        int area = 1;
        for (int[] d : direction) {
            area += dfs(grid, i + d[0], j + d[1]);
        }
        return area;
    }
}
```





回文链表：前面的较短



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
        slow = reverse(slow);
        return isEqual(head, slow);


    }

    private void cut(ListNode node1, ListNode node2) {
        while (node1.next != node2) {
            node1 = node1.next;
        }
        node1.next = null;
    }

    private ListNode reverse(ListNode node) {
        ListNode pre = null;
        while (node != null) {
            ListNode next = node.next;
            node.next = pre;
            pre = node;
            node = next;
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







随机指针

移动指针

指针可能破坏，所以有先后顺序



```java
 Node newNode = tempNode.next;
            
            tempNode.next = tempNode.next.next;
            tempNode = tempNode.next;
            newNode.next = newNode.next != null ? newNode.next.next : null;
```





```java
class Solution {
    public Node copyRandomList(Node head) {
        Node tempNode = head;
        while (tempNode != null) {
            Node newNode = new Node(tempNode.val);
            newNode.next = tempNode.next;
            tempNode.next = newNode;
            tempNode = newNode.next;
        }

        tempNode = head;
        while (tempNode != null) {
            Node newNode = tempNode.next;
            newNode.random = tempNode.random != null ? tempNode.random.next : null;
            tempNode = newNode.next;
        }

        tempNode = head;
        Node resNode = head.next;

        while (tempNode != null) {
            Node newNode = tempNode.next;
            
            tempNode.next = tempNode.next.next;
            tempNode = tempNode.next;
            newNode.next = newNode.next != null ? newNode.next.next : null;
            
            
        }
        return resNode;
    }
}
```







### 最小栈

```java

class MinStack {

    Stack<Integer> stack = new Stack<>();
    Stack<Integer> minStack = new Stack<>();

    /** initialize your data structure here. */
    public MinStack() {
        minStack.push(Integer.MAX_VALUE);
    }
    
    public void push(int val) {
        stack.push(val);
        minStack.push(Math.min(minStack.peek(), val));
    }
    
    public void pop() {
        stack.pop();
        minStack.pop();
    }
    
    public int top() {
        return stack.peek();
    }
    // 不需要做特殊处理，因为可能输入Integer.MAX_VALUE
    public int getMin() {
        return minStack.peek();
    }
}
```



在Node中的构造函数

vlaue写错了

```java
public Node(int key, int vlaue) { 
    this.key = key;
    this.value = value;
}
```





```java
class LRUCache {

    class Node {
        int key;
        int value;
        Node pre;
        Node next;
        public Node(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }

    Node head;
    Node tail;
    int capacity;
    int size = 0;
    Map<Integer, Node> cache = new HashMap<>();

    public LRUCache(int capacity) {
        this.capacity = capacity;
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head.next = tail;
        tail.pre = head;
    }
    
    public int get(int key) {
        Node node = cache.get(key);
        if (node == null) {
            return -1;
        }
        moveToHead(node);
        return node.value;
    }
    
    public void put(int key, int value) {
        Node node = cache.get(key);
        if (node != null) {
            node.value = value;
            cache.put(key, node);
            moveToHead(node);
            return;
        }
        node = new Node(key, value);
        cache.put(key, node);
        addToHead(node);
        size++;
        if (size > capacity) {
            Node delNode = removeTail();
            cache.remove(delNode.key);
            size--;
        }
    }


    public void removeNode(Node node) {
        Node pre = node.pre;
        Node next = node.next;
        pre.next = next;
        next.pre = pre;
    }

    public void addToHead(Node node) {
        node.next = head.next;
        node.pre = head;
        head.next.pre = node;
        head.next = node;
    }

    public Node removeTail() {
        Node delNode = tail.pre;
        removeNode(delNode);
        return delNode;
    }

    public void moveToHead(Node node) {
        removeNode(node);
        addToHead(node);
    }
}
```





和为某一值的路径



pathSums.add(new ArrayList<>(pathSum));



```java
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int target) {
        List<List<Integer>> pathSums = new ArrayList<>();
        dfs(pathSums, new ArrayList<>(), root, target);
        return pathSums;
    }

    public void dfs(List<List<Integer>> pathSums, List<Integer> pathSum, TreeNode root, int target) {
        if (root == null) {
            return;
        }
        target -= root.val;
        pathSum.add(root.val);
        if (target == 0 && root.left == null && root.right == null) {
            pathSums.add(new ArrayList<>(pathSum));
            return;
        }
        dfs(pathSums, pathSum, root.left, target);
        dfs(pathSums, pathSum, root.right, target);
        pathSum.remove(pathSum.size() - 1);
    }
}
```





最大的路径

 int left = Math.max(maxGain(root.left), 0);
 int right = Math.max(maxGain(root.right), 0);

提前判断一次

```java
class Solution {
    int maxPathSum = 0;
    public int maxPathSum(TreeNode root) {
        maxGain(root);
        return maxPathSum;
    }

    public int maxGain(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = Math.max(maxGain(root.left), 0);
        int right = Math.max(maxGain(root.right), 0);
        maxPathSum = Math.max(maxPathSum, left + right + root.val);
        return Math.max(root.val + left, root.val + right);
    }
}
```







res = new int[]{map.get(target - nums[i]), i};

不能使用 res = {1, 2};





最接近三数之和

sum < target 不是 sum < 0

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        int res = 100000;
        if (nums == null || nums.length == 0) {
            return res;
        }
        Arrays.sort(nums);
        for (int i = 0; i < nums.length - 2; i++) {
            int l = i + 1;
            int r = nums.length - 1;
            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            while (l < r) {
                int sum = nums[i] + nums[l] + nums[r];
                if (sum == target) {
                    return target;
                }
                if (Math.abs(res - target) > Math.abs(sum - target)) {
                    res = sum;
                }
                if (sum < target) {
                   while (l < r && nums[l] == nums[l + 1]) {
                        l++;
                    }
                    l++;
                } else {
                    while (l < r && nums[r] == nums[r - 1]) {
                        r--;
                    }
                    r--;  
                } 
            }
        }
        return res;
    }
}
```









### 最小的k个数



注意边界分析

```java
 int[] p = paration(arr, l, mid, r);
            if (k - 1 < p[0] + 1) {
                quickSort(arr, 0, p[0], k);
            } else if (k - 1 > p[0] + 1) {
                quickSort(arr, p[0] + 2, r, k);
            } else {
                return;
            }
```







```java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        quickSort(arr, 0, arr.length - 1, k);
        int[] res = new int[k];
        for (int i = 0; i < k; i++) {
            res[i] = arr[i];
        }
        return res;
    }

    public void swap(int[] arr, int i, int j) {
        if (i == j) {
            return;
        }
        arr[i] = arr[i] ^ arr[j];
        arr[j] = arr[i] ^ arr[j];
        arr[i] = arr[i] ^ arr[j];
    }

    public void quickSort(int[] arr, int l, int r, int k) {
        if (l < r) {
            int mid = l + (r - l) / 2;
            int[] p = paration(arr, l, mid, r);
            if (k - 1 < p[0] + 1) {
                quickSort(arr, 0, p[0], k);
            } else if (k - 1 > p[0] + 1) {
                quickSort(arr, p[0] + 2, r, k);
            } else {
                return;
            }
 
        }
    }

    public int[] paration(int[] arr, int l, int mid, int r) {
        int less = l - 1;
        int more = r;
        while(l < more) {
            if (arr[l] < arr[r]) {
                swap(arr, ++less, l++);
            } else if (arr[l] > arr[r]) {
                swap(arr, l, --more);
            } else {
                l++;
            }
        }
        swap(arr, l, r);
        return new int[]{less, more + 1};

    }

}
```



### 二进制反转



方法中变量需要用户手动初始化

map.containsKey() // K

数据类型是否定义

方法名是否正确







IP地址复原

0xx:不允许出现

```java

if (i != 0 && s.charAt(0) == '0') {
                break;
            }
```







```java

class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> restoreList = new ArrayList<>();
        doRestore(restoreList, new StringBuilder(), s, 0);
        return restoreList; 
    }

    public void doRestore(List<String> restoreList, StringBuilder str, String s, int index) {
        if (index == 4 || s.length() == 0) {
            if (index == 4 && s.length() == 0) {
                restoreList.add(new String(str));
            }
            return;
        }

        for (int i = 0; i <= 2 && i < s.length(); i++) {
            if (i != 0 && s.charAt(0) == '0') {
                break;
            }
            String part = s.substring(0, i + 1);
            if (Integer.parseInt(part) <= 255) {
                if (str.length() != 0) {
                    part = "." + part;
                }
                str.append(part);
                doRestore(restoreList, str, s.substring(i+1), index + 1);
                str.delete(str.length() - part.length(), str.length());
            }
        }
    }
}
```











### 运算符优先级



String 方法

list常用方法

System.arrayCopy



输入输出







int res = 1

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int[] dp = new int[nums.length];
        Arrays.fill(dp, 1);
        int res = 1;
        for (int i = 1; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            res = Math.max(res, dp[i]);
        }
        return res;

    }
}
```



r = len

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int len = 0;
        int[] dp = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            int index = binarySearch(dp, nums[i], len);
            dp[index] = nums[i];
            if (index == len) {
                len++;
            }
        }
        return len;
    }

    public int binarySearch(int[] dp, int num, int len) {
        int l = 0;
        int r = len;
        
        while (l < r) {
            int mid = l + (r - l) / 2;
            if (num == dp[mid]) {
                return mid;
            } else if (num > dp[mid]) {
                l = mid + 1;
            } else {
                r= mid;
            }
        }
        return l;
    }
 

}
```





0[], 7[]



```java
  if (coins == null) {
            return 0;
  }
```





```java

class Solution {
    public int change(int amount, int[] coins) {

        if (coins == null) {
            return 0;
        }
        int len = coins.length;
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



### 最长有效括号



```java
class Solution {
    public int longestValidParentheses(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        Stack<Integer> stack = new Stack<>();
        stack.push(-1);
        int res = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                stack.pop();
                if (stack.isEmpty()) {
                    stack.push(i);
                } else {
                    res = Math.max(res, i - stack.peek());
                }
            }
        }
        return res;


    }
}
```

max = Math.max(max, dp[i]);

它并不知道取哪一段

s.charAt(i - dp[i - 1] - 2) == ')' ：忘记判断

```java

class Solution {
    public int longestValidParentheses(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        int max = 0;
        int[] dp = new int[s.length()];
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == ')') {
                if (s.charAt(i - 1) == '(') {
                dp[i] = 2 + (i >= 2 ? dp[i - 2] : 0);
                } else if (i - dp[i - 1] - 1 >= 0 && s.charAt(i - dp[i - 1] - 1) == '(') {
                    dp[i] = dp[i - 1] + 2 + (i - dp[i - 1] - 2 > 0 &&
                        s.charAt(i - dp[i - 1] - 2) == ')' ? dp[i - dp[i - 1] - 2] : 0);
                }

            }
            max = Math.max(max, dp[i]);
            
        }
        return max;

    }
}
```







### K笔交易

k<=0,不能有int[0]数组越界

 for (int i = 0; i < k; i++) {
            dp[i][1] = Integer.MIN_VALUE;
 }

0肯定比负数大

```java
class Solution {
    public int maxProfit(int k, int[] prices) {
        if (prices == null || prices.length < 2 || k <= 0) {
            return 0;
        }

        if (k > prices.length / 2) {
            return maxProfit(prices);
        }
       
        int maxProfit = 0;
        int[][] dp = new int[k][2];
        for (int i = 0; i < k; i++) {
            dp[i][1] = Integer.MIN_VALUE;
        }
        for(int price : prices) {
            for (int i = 0; i < k; i++) {
                if (i == 0) {
                    dp[0][0] = Math.max(dp[0][0], dp[0][1] + price);
                    dp[0][1] = Math.max(dp[0][1], -price);
                } else {
                    dp[i][0] = Math.max(dp[i][0], dp[i][1] + price);
                    dp[i][1] = Math.max(dp[i][1], dp[i - 1][0] - price);
                }
            }
        }
        maxProfit = dp[0][0];
        for (int i = 1; i < k; i++) {
            if (maxProfit < dp[i][0]) {
                maxProfit = dp[i][0];
            }
        }
        return maxProfit;

    }

    public int maxProfit(int[] prices) {
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

