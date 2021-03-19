

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













### 运算符优先级



String 方法

list常用方法

System.arrayCopy



输入输出



