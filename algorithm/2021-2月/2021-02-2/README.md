# 2021-02-2



### 题目

| 题目编号 | 题目                                   | 题目链接                                                     | leetcode对应题目 |
| -------- | -------------------------------------- | ------------------------------------------------------------ | ---------------- |
| NC30     | 数组中未出现的最小正整数               | https://www.nowcoder.com/practice/8cc4f31432724b1f88201f7b721aa391?tpId=117&&tqId=35069&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |                  |
| NC36     | 在两个长度相等的排序数组中找到上中位数 | https://www.nowcoder.com/practice/6fbe70f3a51d44fa9395cfc49694404f?tpId=117&&tqId=35071&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |                  |
| NC16     | 判断二叉树是否对称                     | https://www.nowcoder.com/practice/1b0b7f371eae4204bc4a7570c84c2de1?tpId=117&&tqId=34937&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |                  |
| NC69     | 链表中倒数第k个结点                    | https://www.nowcoder.com/practice/529d3ae5a407492994ad2a246518148a?tpId=117&&tqId=34991&rp=1&ru=/activity/oj&qru=/ta/job-code-high/question-ranking |                  |

NC30

```java
public class Solution {
    /**
     * return the min number
     * @param arr int整型一维数组 the array
     * @return int整型
     位运算!!!!!! 异或两次等于原值！！！！！
     */
    public int minNumberdisappered (int[] arr) {
        // write code here
      	int res = 0;
        for(int num : arr){
            if(num > 0)
            	res ^= num;
        }
        for(int i = 1; i <= arr.length;i++){
            res ^= i;
        }
        return res ==0? arr.length+1 : res;
    }
}
```

NC36：



```java
public class Solution {
    /**
     * find median in two sorted array
     * @param arr1 int整型一维数组 the array1
     * @param arr2 int整型一维数组 the array2
     * @return int整型
     */
    public int findMedianinTwoSortedAray (int[] arr1, int[] arr2) {
        // write code here
        for(int i = arr1.length - 1; i >0 ; i/=2){
            if(arr1[i])
        }
    }
}
```

NC16

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



NC69

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

