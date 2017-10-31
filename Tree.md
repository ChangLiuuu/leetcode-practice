
# --------Tag: Tree---------

## 10.30

### 538. Convert BST to Greater Tree
```
 public void helper(TreeNode cur) {
        if (cur == null) return;
        helper(cur.right);
        sum += cur.val;
        cur.val = sum;
        helper(cur.left);
    }

```
* 递归的思路，不需要考虑递归的每一步怎么走，会从代码中，先知道操作，再考虑遍历顺序。
* 操作： sum+=cur.val cur.val记录此时的sum 
* 遍历顺序： 先到最右下子树的cur.right, 再 cur, 接着 cur.left 都进行相同操作。 


