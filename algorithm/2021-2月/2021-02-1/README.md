# 2021-02-1



### 题目

| 题目编号 | 题目                                   | 题目链接                                                     |
| -------- | -------------------------------------- | ------------------------------------------------------------ |
| NC5      | 二叉树根节点到叶子节点的所有路径和     | https://www.nowcoder.com/practice/185a87cd29eb42049132aed873273e83?tpId=117&&tqId=34926&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |
| NC8      | 二叉树根节点到叶子节点和为指定值的路径 | https://www.nowcoder.com/practice/840dd2dc4fbd4b2199cd48f2dadf930a?tpId=117&&tqId=34929&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |
| NC21     | 链表内指定区间反转                     | https://www.nowcoder.com/practice/b58434e200a648c589ca2063f1faf58c?tpId=117&&tqId=34942&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |
| NC73     | 数组中出现次数超过一半的数字           | https://www.nowcoder.com/practice/e8a1b01a2df14cb2b228b30ee6a92163?tpId=117&&tqId=34995&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |


NC5:

```java
public class Solution {
    /**
     *
     * @param root TreeNode类
     * @return int整型
     */
    int sum =0;
    public int sumNumbers (TreeNode root) {
        // write code here
        if(root == null) return 0;

        return roadAddSum(root,root.val);
    }
    public int roadAddSum(TreeNode root,int sum){

        if(root.left == null && root.right ==null){
            return sum;
        }
        int res = 0;
        if(root.left!=null) {
            res += roadAddSum(root.left,sum*10+root.left.val);
        }

        if(root.right!=null) {
            res += roadAddSum(root.right,sum*10+root.right.val);
        }
        return res;
    }
}
```

NC8:

```java
//注意sum为负数的情况！！！
public class Solution {
    ArrayList<ArrayList<Integer>> res = new ArrayList<>();
    public ArrayList<ArrayList<Integer>> pathSum (TreeNode root, int sum) {
        // write code here
        ArrayList<Integer> tmp = new ArrayList<>();
        findPath(root,sum,tmp);
        return res;
    }
    public void findPath(TreeNode root, int sum,ArrayList<Integer> tmp ){
        if(root == null) return;
        sum-=root.val;
        tmp.add((Integer)root.val);
        if( root.left == null &&  root.right == null&& sum == 0 ){
            res.add(new ArrayList(tmp));//直接加后续修改时也会变化
            tmp.remove(tmp.size()-1);
            return;
        }
        findPath(root.left,sum,tmp);
        findPath(root.right,sum,tmp);
        tmp.remove(tmp.size()-1);//一定要在这里加一句

    }
}
```

NC21:

```java
public class Solution {
    /**
     *
     * @param head ListNode类
     * @param m int整型
     * @param n int整型
     * @return ListNode类
     *///刷题一定要注意只有一个结点，没有节点 这些特殊情况。
    //写链表题一定考虑空指针问题！！！
    public ListNode reverseBetween (ListNode head, int m, int n) {
        // write code here
        if(head == null||m==n) return head;
        ListNode h = new ListNode(-1);//pre作为链接时的节点的前一系欸DNA
        ListNode pre = h;//返回时要得到头节点，但是逆序头节点可能变化，所以保存头节点的前一结点，返回h.next即可得到合适的头节点
        pre.next = head;//存储前一结点，方便在反转后链接上;返回pre.nextf防止出错
        int count = 1;
        while(head != null && count < m ){
            pre = head;
            head = head.next;
            count ++;
        }
        //将第一个需要逆反的结点拿出来方便后续链接
        ListNode comp = null;//是已经完成逆序的第一个节点
        ListNode tmp = null;
        while(count <=n && head!=null){
            tmp = head.next;//tmp是剩余未完成逆序的第一个节点
            head.next = comp;
            comp = head;
            head = tmp;
            count ++;
        }
        pre.next = comp;
        while(comp.next!=null){
            comp = comp.next;
        }
        comp.next = tmp;
        return h.next;
    }
}
```



NC73:

```java
import java.util.*;
public class Solution {
    public int MoreThanHalfNum_Solution(int [] array) {
        if(array.length == 0) return  0;
        HashMap<Integer,Integer> map = new HashMap<>();
        int maxTimesKey = array[0];//注意有一个元素的情况
        int maxTimes = 1;
        for (int c: array) {
            if(map.containsKey(c)){
                map.put(c,map.get(c)+1);
                if(map.get(c) > maxTimes){
                    maxTimes = map.get(c);
                    maxTimesKey = c;
                }
            }else{//当只有一个元素时会直接进入到这里，若maxTimes和maxTimesKey没有赋值，则返回值会出现错误。
                map.put(c,1);
            }
        }
        if(maxTimes > array.length/2) return maxTimesKey;
        return 0;
    }
}
```

