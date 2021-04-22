# Binary Tree
[Reference URL](https://www.cnblogs.com/idorax/p/6441043.html)

## 1. 树(Tree)的基本概念
### 1.1 树的定义
A tree is a (possibly non-linear) data structure made up of nodes or vertices and edges without having any cycle. The tree with no nodes is called the null or empty tree. A tree that is not empty consists of a root node and potentially many levels of additional nodes that form a hierarchy.
树是由结点或顶点和边组成的(可能是非线性的)且不存在着任何环的一种数据结构。没有结点的树称为空(null或empty)树。一棵非空的树包括一个根结点，还(很可能)有多个附加结点，所有结点构成一个多级分层结构。

[注：本文将node一律译为"结点"(而不是"节点")，因为joint或connection是节点，而node是结点。关于"结点"与"节点"请自行搜索浙江大学陈水福教授的文章--"360度"解读如何正确应用"结点"与"节点"]
## 2. 二叉树（Binary Tree)
### 2.1 什么是二叉树（Binary Tree)
每个结点至多拥有两棵子树(即二叉树中不存在度大于2的结点)，并且，二叉树的子树有左右之分，其次序不能任意颠倒。
### 2.2 二叉树的性质
（1）若二叉树的层次从0开始，则在二叉树的第i层至多有2^i个结点(i>=0)。

（2）高度为k的二叉树最多有2^(k+1) - 1个结点(k>=-1)。 (空树的高度为-1)

（3）对任何一棵二叉树，如果其叶子结点(度为0)数为m, 度为2的结点数为n, 则m = n + 1。
### 2.3 完美二叉树(Perfect Binary Tree)
A Perfect Binary Tree(PBT) is a tree with all leaf nodes at the same depth. All internal nodes have degree 2.
一个深度为k(>=-1)且有2^(k+1) - 1个结点的二叉树称为完美二叉树。 (注： 国内的数据结构教材大多翻译为"满二叉树")
例如：  
![](https://meirongding.github.io/notes/images/perfect%20binary%20tree.png)
### 2.4 完全二叉树(Complete Binary Tree)
A Complete Binary Tree （CBT) is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.
换句话说，完全二叉树从根结点到倒数第二层满足完美二叉树，最后一层可以不完全填充，其叶子结点都靠左对齐。

例如：  
![](https://meirongding.github.io/notes/images/complete%20binary%20tree.png)
### 2.5 完满二叉树(Full Binary Tree)
A Full Binary Tree (FBT) is a tree in which every node other than the leaves has two children.
换句话说，所有非叶子结点的度都是2。（只要你有孩子，你就必然是有两个孩子。） 

注：Full Binary Tree又叫做Strictly Binary Tree。

例如：  
![](https://meirongding.github.io/notes/images/full%20binary%20tree.png)
### 2.6 完美(Perfect)二叉树 v.s. 完全(Complete)二叉树
（1） 一棵完美(Perfect)二叉树看起来是这个样儿的， 【图2.6.1】

![](https://meirongding.github.io/notes/images/perfect%20tree.png)

（2） 那么，将编号为15, 14, ..., 9的叶子结点从右到左依次拿掉或者拿掉部分，则是一棵完全(Complete)二叉树,
例如，将上图中的编号为15, 14, 13, 12, 11叶子结点都拿掉(从右到左的顺序)， 【图2.6.2】

![](https://meirongding.github.io/notes/images/complete%20tree.png)

（3） 下图就不是一棵完全(Complete)二叉树，【图2.6.3】，

如果将编号11(K)结点从编号6(E)的左儿子位置移动到编号5(E)的右儿子位置，则变成一棵完全(Complete)二叉树。

![](https://meirongding.github.io/notes/images/complete%20tree%20false.png)

注： 图2.6.1， 2.6.2和2.6.3将Full Binary Tree当做就是Perfect Binary Tree, 我认为是不正确的，特此说明。

特别说明： 其实，理解完全(Complete)二叉树可以借助于栈(stack)的思想。  
例如，把图2.6.1中的完美(Perfect)二叉树的所有结点按照编号1, 2, 3, ..., 15依次入栈(push)。  
那么，对栈的每一次出栈(pop)操作后，栈里保存的结点集对应到图2.6.1上去都是一棵完全(Complete)二叉树。
### 2.7 完全(Complete)二叉树 v.s. 完满(Full)二叉树
![](https://meirongding.github.io/notes/images/full%20and%20complete%20binary%20tree.png)
### 2.8 完满(Full)二叉树 v.s. 完全(Complete)二叉树 v.s. 完美(Perfect)二叉树
![](https://meirongding.github.io/notes/images/full%20and%20complete%20and%20perfect%20binary%20tree.png)
## 3. 总结 (下表参考来源)
完美二叉树	Perfect Binary Tree  

Every node except the leaf nodes have two children and every level (last level too) is completely filled.  
除了叶子结点之外的每一个结点都有两个孩子，每一层(当然包含最后一层)都被完全填充。

完全二叉树	Complete Binary Tree  

Every level except the last level is completely filled and all the nodes are left justified.  
除了最后一层之外的其他每一层都被完全填充，并且所有结点都保持向左对齐。

完满二叉树	Full/Strictly Binary Tree  

Every node except the leaf nodes have two children.  
除了叶子结点之外的每一个结点都有两个孩子结点。

**完美(Perfect)二叉树一定是完全(Complete)二叉树，但完全(Complete)二叉树不一定是完美(Perfect)二叉树。**  
**完美(Perfect)二叉树一定是完满(Full)二叉树，但完满(Full)二叉树不一定是完美(Perfect)二叉树。**  
**完全(Complete)二叉树可能是完满(Full)二叉树，完满(Full)二叉树也可能是完全(Complete)二叉树。**  
**既是完全(Complete)二叉树又是完满(Full)二叉树也不一定就是完美(Perfect)二叉树。**