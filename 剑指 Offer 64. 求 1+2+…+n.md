## 剑指 Offer 64. 求 1+2+…+n

<p>求 <code>1+2+...+n</code> ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入:</strong> n = 3
<strong>输出:&nbsp;</strong>6
</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入:</strong> n = 9
<strong>输出:&nbsp;</strong>45
</pre>

<p><strong>限制：</strong></p>
	<li><code>1 &lt;= n&nbsp;&lt;= 10000</code></li>


---

> &ensp;&ensp;打开leetcode
> &ensp;&ensp;&ensp;&ensp;嗯……这题……这也不能用，那也不能用……
> &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;(^_^) 关闭leetcode  
> &ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;&ensp;睡觉！

## 那肯定是不行的！##

### 想了好久也没有思路……猜测是不是可以用位运算符？###

#### 阿巴阿巴阿巴阿巴？ 好的，今天抄作业！（理不直气不壮） ####


**正文开始**
---

梳理了一下题解区的答案，大概分为三种：

1. [逻辑运算符的短路效应](#jump1) （太强啦！
2. [俄罗斯农民乘法](#jump2)	  （emm这个没看懂，不懂位运算符的原理，需要补课
3. [异常捕获法](#jump3)		  （秀得我头皮发麻

下面是三种方法的代码实现与分析

### <span id="jump1">**1. 逻辑运算符的短路效应**</span> ：

> 以逻辑运算符 `&&` 为例：
> &ensp;&ensp;&ensp;&ensp;对于 `A && B` 这个表达式，如果 `A` 表达式返回 `False` ，那么 `A && B` 已经确定为 `False` ，此时不会去执行表达式 `B`。
> &ensp;&ensp;&ensp;&ensp;同理，对于逻辑运算符 `||`， 对于 `A || B` 这个表达式，如果 `A` 表达式返回 `True` ，那么 `A || B` 已经确定为 `True` ，此时不会去执行表达式 `B`。

> 利用这一特性：
> &ensp;&ensp;&ensp;&ensp;当使用`&&`时，将递归的返回条件取非然后作为 `&&` 的**第一个条件语句**，递归的主体转换为**第二个条件语句**，当递归的返回条件为 `true` 的情况下就不会执行递归的主体部分，递归返回。
> &ensp;&ensp;&ensp;&ensp;当使用`||`时，将递归的返回条件n=0作为`||`的**第一个条件语句**，递归的主体转换为**第二个条件语句**，当递归的返回条件为`false`的情况下就不会执行递归的主体部分，递归返回。

```java
class Solution {
    public int sumNums(int n) {
        boolean flag = n > 0 && (n += sumNums(n - 1)) > 0;
        return n;
    }
}
```

```java
class Solution {
    public int sumNums(int n) {
        boolean flag = (n == 0) || (n += sumNums(n - 1)) > 0;
        return n;
    }
}
```
### <span id="jump2">**2. 俄罗斯农民乘法**</span> ：

> 这个是真的没看懂……就先贴一下代码吧，回头看懂了再补上自己的分析

```java
class Solution {
    /**
     * 负数在参与位运算时使用的是补码
     * -1的原码是   10000000 00000000 00000000 00000001
     * -1的反码是   11111111 11111111 11111111 11111110
     * -1的补码是   11111111 11111111 11111111 11111111
     * 因此任何数与-1做与运算的结果任然为原数
     */
    public int sumNums(int n) {
        /**
         * 由等差数列求和公式可知，结果等于n*(n+1)/2，其中除以2可以通过右移1位进行操作
         * 但n*(n+1)在不允许使用乘法的情况下，只能把n或n+1其中一个拆解为2的n次幂数之和，配合另一个来进行位运算和累加
         * 此代码利用了-1和任何整数进行与运算还等于原数的特点
         * -(n + 1 >> 0 & 1)用于求从低到高第i+1位如果为0取，如果为1取-1
         */
        int n1 = (n & -(n + 1 >> 0 & 1)) << 0;
        int n2 = (n & -(n + 1 >> 1 & 1)) << 1;
        int n3 = (n & -(n + 1 >> 2 & 1)) << 2;
        int n4 = (n & -(n + 1 >> 3 & 1)) << 3;
        int n5 = (n & -(n + 1 >> 4 & 1)) << 4;
        int n6 = (n & -(n + 1 >> 5 & 1)) << 5;
        int n7 = (n & -(n + 1 >> 6 & 1)) << 6;
        int n8 = (n & -(n + 1 >> 7 & 1)) << 7;
        int n9 = (n & -(n + 1 >> 8 & 1)) << 8;
        int n10 = (n & -(n + 1 >> 9 & 1)) << 9;
        int n11 = (n & -(n + 1 >> 10 & 1)) << 10;
        int n12 = (n & -(n + 1 >> 11 & 1)) << 11;
        int n13 = (n & -(n + 1 >> 12 & 1)) << 12;
        int n14 = (n & -(n + 1 >> 13 & 1)) << 13;
        return (n1 + n2 + n3 + n4 + n5 + n6 + n7 + n8 + n9 + n10 + n11 + n12 + n13 + n14) >> 1;
    }
}

作者：shitsurei
链接：https://leetcode-cn.com/problems/qiu-12n-lcof/solution/yan-jiu-liao-ban-tian-zhong-yu-kan-dong-da-lao-de-/

```

感兴趣的也可以参考leetcode的官方题解。
链接：https://leetcode-cn.com/problems/qiu-12n-lcof/solution/qiu-12n-by-leetcode-solution/

### <span id="jump3"> ** 3. 异常捕获法 ** </span> ：


这波操作是真滴强，真的是“一个人被逼急了真的什么代码都敲得出来”hhhhhh

解析：
&ensp;&ensp;&ensp;&ensp; 首先定义了一个只有一个元素的数组（此时数组中只有test[0]可以访问），然后进入算法内部，进行try_catch。在尝试返回test[n]时，因为传入参数大于等于0，所以只有在n=0时，才会成功返回，即：触发了递归终止的条件。否则，catch异常，执行递归语句。

```java
class Solution {
    int[] test=new int[]{0};
    public int sumNums(int n) {
        try{
            return test[n];
        }catch(Exception e){
            return n+sumNums(n-1);
        }
    }
}
```

## 最后

因为这道题的解法都不是自己写的，所以就不提交到leetcode去污染提交正确率了 ^_^

