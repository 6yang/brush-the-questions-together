# 2021-01-25



### 题目

| NC112 | https://www.nowcoder.com/practice/2cc32b88fff94d7e8fd458b8c7b25ec1?tpId=190&&tqId=35410&rp=1&ru=/activity/oj&qru=/ta/job-code-high-rd/question-ranking |
| ----- | ------------------------------------------------------------ |
| NC137 | https://www.nowcoder.com/practice/c215ba61c8b1443b996351df929dc4d4?tpId=190&&tqId=36043&rp=1&ru=/activity/oj&qru=/ta/job-code-high-rd/question-ranking |
| NC12  | https://www.nowcoder.com/practice/8a19cbe657394eeaac2f6ea9b0f6fcf6?tpId=190&&tqId=35426&rp=1&ru=/activity/oj&qru=/ta/job-code-high-rd/question-ranking |
| NC7   | https://www.nowcoder.com/practice/64b4262d4e6d4f6181cd45446a5821ec?tpId=190&&tqId=35181&rp=1&ru=/activity/oj&qru=/ta/job-code-high-rd/question-ranking |



## NC112

```java
public String solve(int M, int N) {
        // write code here
        if (M == 0) {
            return "0";
        }
        boolean sign = false;
        if (M < 0) {
            sign = true;
            M = -M;
        }
        StringBuilder sb = new StringBuilder();
        while (M > 0) {
            int k = M % N;
            if (k >= 10) {
                sb.append((char) (k - 10 + 'A'));
            } else {
                sb.append(k);
            }
            M /= N;
        }
        if (sign) {
            sb.append("-");
        }
        return sb.reverse().toString();
    }
```

## NC137

```java
public int solve(String s) {
        // write code here
        Stack<Integer> stack = new Stack<>();
        int num = 0, sum = 0;
        char sign = '+'; // 默认第一个为+
        char[] arr = s.toCharArray();
        int n = s.length();
        for (int i = 0; i < n; i++) {
            char c = arr[i];
            if (c == '(') {
                int j = i + 1;
                int countPar = 1;
                while (countPar > 0) {
                    if (arr[j] == '(') {
                        countPar++;
                    }
                    if (arr[j] == ')') {
                        countPar--;
                    }
                    j++;
                }
                num = solve(s.substring(i + 1, j - 1));
                i = j - 1; //for 后面还有一个i++
            }
            if (Character.isDigit(c)) {
                num = num * 10 + c - '0';
            }
            if (!Character.isDigit(c) || i == n - 1) {
                if (sign == '+') {
                    stack.push(num);
                } else if (sign == '-') {
                    stack.push(-1 * num);
                } else if (sign == '*') {
                    stack.push(stack.pop() * num);
                } else if (sign == '/') {
                    stack.push(stack.pop() / num);
                }
                num = 0;
                sign = c;
            }
        }
        while (!stack.isEmpty()) {
            sum += stack.pop();
        }
        return sum;
    }
```

## NC12

```java
HashMap<Integer, Integer> map = new HashMap<>();
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        for (int i = 0; i < inorder.length; i++) {
            map.put(inorder[i],i);
        }
        return build(preorder,0,preorder.length-1,inorder,0,inorder.length-1);
    }
    public TreeNode build(int [] preOrder,int preL,int preR,int [] inOrder,int inL,int inR){
        if(preL>preR||inL>inR) return null;
        TreeNode root = new TreeNode(preOrder[preL]);
        int inCenter = map.get(preOrder[preL]);
        int inLeftSize = inCenter - inL;
        root.left = build(preOrder,preL+1,preL+inLeftSize,inOrder,inL,inCenter-1);
        root.right = build(preOrder,preL+inLeftSize+1,preR,inOrder,inCenter+1,inR);
        return root;
    }
```

