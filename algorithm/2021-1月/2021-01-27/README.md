# 2021-01-27



### 题目

| NC140 | 排序，所有的排序算法       | https://www.nowcoder.com/practice/2baf799ea0594abd974d37139de27896?tpId=117&&tqId=36039&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |
| ----- | -------------------------- | ------------------------------------------------------------ |
| NC141 | 判断回文                   | https://www.nowcoder.com/practice/e297fdd8e9f543059b0b5f05f3a7f3b2?tpId=117&&tqId=36040&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |
| NC59  | 矩阵的最小路径和           | https://www.nowcoder.com/practice/7d21b6be4c6b429bb92d219341c4f8bb?tpId=117&&tqId=35078&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |
| NC96  | 判断一个链表是否为回文结构 | https://www.nowcoder.com/practice/3fed228444e740c8be66232ce8b87c2f?tpId=117&&tqId=35018&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |



## NC141 判断回文

```java
public boolean judge(String str) {
        // write code here
        if (str == null || str.length() < 2) {
            return true;
        }
        int left = 0;
        int right = str.length() - 1;
        while (left < right) {
            if(str.charAt(left++)!=str.charAt(right--)) return false;
        }
        return true;
    }
```



## NC59 矩阵的最小路径和

```JAVA
public int minPathSum(int[][] matrix) {
        // write code here
        int m = matrix.length;
        int n = matrix[0].length;
        for (int i = 1; i < m; i++) {
            matrix[i][0] += matrix[i-1][0];
        }
        for (int i = 1; i < n; i++) {
            matrix[0][i] += matrix[0][i-1];
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                matrix[i][j] += Math.min(matrix[i-1][j],matrix[i][j-1]);
            }
        }
        return matrix[m-1][n-1];
    }
```



## NC96 判断一个链表是否为回文结构

```java
public boolean isPail(ListNode head) {
        // write code here
        if (head == null || head.next == null) {
            return true;
        }
        ListNode slow = head;
        ListNode fast = head;
        ListNode pre= null  ,p = null;
        while (fast != null && fast.next != null) {
            p = slow;
            slow = slow.next;
            fast = fast.next.next;
            p.next = pre;  // 翻转前半部分
            pre = p;
        }
        if(fast != null) {  //  如果是奇数个节点跳过奇数节点
            slow = slow.next;
        }
        while(p!=null){
            if(p.val != slow.val){
                return false;
            }
            p = p.next;
            slow = slow.next;
        }
        return true;
    }
```

