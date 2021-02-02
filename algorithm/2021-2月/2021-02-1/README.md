# 2021-02-1



### 题目

| 题目编号 | 题目                                   | 题目链接                                                     | leetcode对应题目 |
| -------- | -------------------------------------- | ------------------------------------------------------------ | ---------------- |
| NC5      | 二叉树根节点到叶子节点的所有路径和     | https://www.nowcoder.com/practice/185a87cd29eb42049132aed873273e83?tpId=117&&tqId=34926&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking | 129              |
| NC8      | 二叉树根节点到叶子节点和为指定值的路径 | https://www.nowcoder.com/practice/840dd2dc4fbd4b2199cd48f2dadf930a?tpId=117&&tqId=34929&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking | 剑指offer34      |
| NC21     | 链表内指定区间反转                     | https://www.nowcoder.com/practice/b58434e200a648c589ca2063f1faf58c?tpId=117&&tqId=34942&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |                  |
| NC73     | 数组中出现次数超过一半的数字           | https://www.nowcoder.com/practice/e8a1b01a2df14cb2b228b30ee6a92163?tpId=117&&tqId=34995&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking | 剑指offer39      |



## NC5 二叉树根节点到叶子节点的所有路径和

```java
public int sumNumbers (TreeNode root) {
        // write code here
        return getSum(root , 0);
    }

    private int getSum(TreeNode root, int i) {
        if (root == null ) return 0;
        int temp = root.val + i*10;
        if(root.left == null && root.right == null){
            return temp;
        }
        return getSum(root.left,temp) + getSum(root.right,temp);
    }
```

## NC8 二叉树根节点到叶子节点和为指定值的路径

```java
ArrayList<ArrayList<Integer>> res = new ArrayList<>();
    ArrayList<Integer> path = new ArrayList<>();

    public ArrayList<ArrayList<Integer>> pathSum(TreeNode root, int sum) {
        // write code here
        if (root == null) {
            return res;
        }
        dfs(root, sum);
        return res;
    }

    private void dfs(TreeNode root, int sum) {
        if (root == null) {
            return;
        }
        if (root.left == null && root.right == null) {
            if (sum - root.val == 0) {
                path.add(root.val);
                res.add(new ArrayList<>(path));
                path.remove(path.size() - 1);
            }
            return;
        }
        path.add(root.val);
        dfs(root.left, sum - root.val);
        dfs(root.right, sum - root.val);
        path.remove(path.size() - 1);
    }
```

## NC21 链表内指定区间反转

```java
public ListNode reverseBetween (ListNode head, int m, int n) {
        // write code here
        if (head == null ) return null;
        ListNode res = new ListNode(-1);
        res.next = head;
        ListNode pre = res;
        for (int i = 1; i < m; i++) {
            pre = pre.next;
        }
        ListNode cur = pre.next;
        ListNode curNext = cur.next;
        for (int i = m; i < n; i++) {
            cur.next = curNext.next;
            curNext.next = pre.next;
            pre.next = curNext;
            curNext = cur.next;
        }
        return res.next;
    }
```

## NC79 数组中出现次数超过一半的数字

```java
// 解法   1 hash
    //       2 排序
    //       3 摩尔投票法
    public int MoreThanHalfNum_Solution(int [] array) {
        int x = 0 ,vote = 0 ,count = 0;
        for (int num : array) {
            if(vote == 0) x = num;
            vote += num == x ? 1 : -1;
        }
        for (int num : array) {
            if(num == x) count++;
        }
        return count > array.length/2 ? x : 0;
    }
```

