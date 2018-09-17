tags:
- 二叉树
- 中序遍历

### 二叉搜索树的第k个结点
给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4。
```cpp
//递归法
TreeNode* KthNode(TreeNode* pRoot, int k)
{
    if(!pRoot || k < 0)
        return NULL;
    return inorderBiTree(pRoot, k);
}

TreeNode* inorderBiTree(TreeNode* node, int& k)
{
    if(!node) return NULL;
    TreeNode* result = inorderBiTree(node->left, k);
    if(result)    return result;
    k--;
    if(k == 0)
        return node;
    return inorderBiTree(node->right, k);
}

//迭代法
TreeNode* KthNode(TreeNode* pRoot, int k)
{
    if(!pRoot || k < 0)
        return NULL;
    stack<TreeNode*> visit;
    TreeNode* node = pRoot;
    int count = 0;
    while(node || !visit.empty())
    {
        while(node)
        {
            visit.push(node);
            node = node->left;
        }
        node = visit.top();
        visit.pop();
        count++;
        if(count == k)
            return node;
        node = node->right;
    }
    return NULL;
}
```