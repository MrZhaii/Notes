### [剑指 Offer 06]从尾到头打印链表

#### 问题：

<p>输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。</p>
<p><strong>示例 1：</strong></p>
<pre><strong>输入：</strong>head = [1,3,2]
<strong>输出：</strong>[2,3,1]</pre>
<p><strong>限制：</strong></p>
<p><code>0 &lt;= 链表长度 &lt;= 10000</code></p>

---

#### 个人思路：

- 返回数组，则创建一个数组【疑问：数组长度多少】

- 遍历链表，获取数组长度

- 再次遍历链表，倒着放入数组 

#### 个人代码：

```java
public int[] reversePrint(ListNode head) {
        //链表长度
        int length=0;
        //设置游标
        ListNode p=head;
        ListNode q=head;
        //获取链表长度
        //head [1,3,2]
        while(p!=null){
            length++;
            p=p.next;
        }
        int arr[] = new int[length];
        int index=length-1;
        while(q!=null){
            arr[index]=q.val;
            q=q.next;
            index--;
        }
        return arr;
    }
```

---

#### 他人思路：

栈	【利用栈的后进先出特性】
```java
  public int[] reversePrint(ListNode head) {
        Stack<ListNode> stack = new Stack<ListNode>();  
      	ListNode temp = head;
        while (temp != null) {
            stack.push(temp);
            temp = temp.next;
        }
        int size = stack.size();
        int[] print = new int[size];
        for (int i = 0; i < size; i++) {
            print[i] = stack.pop().val;
        }
        return print;
    }

```

---

递归
  - 递推阶段：每次传入` head.next`,以`head==null`为递归终止条件
    
  - 回溯阶段：层层回溯，将节点值加入列表`tmp`
    
  - 最终阶段：列表转换为数组

```java
class Solution {
    ArrayList<Integer> tmp = new ArrayList<Integer>();
    public int[] reversePrint(ListNode head) {
        recur(head);
        int[] res = new int[tmp.size()];
        for(int i = 0; i < res.length; i++)
            res[i] = tmp.get(i);
        return res;
    }
    void recur(ListNode head){
        //递归终止条件
        if(head==null)
            return;
        // head!=null 进行递归
        recur(head.next);
        // 递归结束，添加值
        tmp.add(head.val);

    }
}
```

---

#### 总结：

- 自己对于数据结构的使用不够熟悉，虽然知道其各自特性是什么，但是在思考问题时并不能第一时间考虑到
- 利用递归解决问题处于完全陌生的状态，对于其过程与终止条件，需要细细考虑