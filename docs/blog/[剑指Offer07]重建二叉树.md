### [剑指 Offer 07]重建二叉树

#### 问题：

<p>输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。</p>
<p>例如，给出</p>
<pre>前序遍历 preorder =&nbsp;[3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]</pre>
<p>返回如下的二叉树：</p>
<pre>    3
   / \
  9  20
    /  \
   15   7</pre>
<p><strong>限制：</strong></p>
<p><code>0 &lt;= 节点个数 &lt;= 5000</code></p>

---

#### 思路：【思考未果，查看大佬思路】

- 分治思想，将大的数组分割成小数组处理
- 在每个数组中递归插入根节点
- 获取中序遍历后左节点个数（假设为n）
- 先序遍历根节点后,n个节点均为左子树节点（数目是相等的）

#### 代码：

```java
class Solution {
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        //先序遍历：[3,9,20,15,7]
        //中序遍历：[9,3,15,20,7]
        //本题利用根节点递归
        int n=preorder.length;
        if(n==0){
            return null;
        }
        //先序遍历第一个位置为根节点
        int root_val=preorder[0];
        int root_index=0;
        for (int i = 0; i < inorder.length; i++) {
            //寻找到在中序排序中的位置
            if(inorder[i]==root_val){
                root_index=i;
                break;
            }
        }
        //创建节点，插入数据
        TreeNode root = new TreeNode(root_val);
        //递归
        //分治思想
        //利用中序遍历中左、右节点个数在先序遍历中也是多少 进行分割
        //分割出来的数组进行递归解决
        root.left=buildTree(Arrays.copyOfRange(preorder,1,1+root_index),Arrays.copyOfRange(inorder,0,root_index));
        root.right=buildTree(Arrays.copyOfRange(preorder,1+root_index,n),Arrays.copyOfRange(inorder,root_index+1,n));
        return root;
    }
}
```

---

#### 总结：

- 树结构以及其各种遍历方式自己都知道，但是面对代码疯狂抓瞎，思路全无，并不能将自己知道的真正实践出来，还需多练