# Construct Binary Search Tree from Preorder Traversal
Return the root node of a binary search tree that matches the given preorder traversal.

(Recall that a binary search tree is a binary tree where for every node, any descendant of `node.left` has a `value` < `node.val`, and any descendant of `node.right` has a `value` > `node.val`.  

Also recall that a preorder traversal displays the value of the node first, then traverses `node.left`, then traverses `node.right`.)

#### Example 
```
Input: [8,5,1,7,10,12]
Output: [8,5,10,1,7,null,12]
```

### C
```C
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     struct TreeNode *left;
 *     struct TreeNode *right;
 * };
 */


struct TreeNode* bstFromPreorder(int* preorder, int preorderSize){
    struct TreeNode *root = malloc(sizeof(struct TreeNode));
    root->val = preorder[0];
    root->left = root->right = NULL;
    
    struct TreeNode *path[100];
    int topIndex = 0;
    path[topIndex] = root;
    
    for(int i = 1; i < preorderSize; i++)
    {
        struct TreeNode *node = malloc(sizeof(struct TreeNode));
        node->val = preorder[i];
        node->left = node->right = NULL;
        
        if(preorder[i] < path[topIndex]->val)
        {
            path[topIndex]->left = node;
            topIndex++;
            path[topIndex] = node;
        }
        else
        {
            while((topIndex >= 1)&&(path[topIndex - 1]->val < preorder[i]))
                topIndex--;
            
            if(topIndex >= 1)
            {
                path[topIndex]->right = node;
                path[topIndex] = node;
            }
            else
            {
                path[0]->right = node;
                path[0] = node;
            }
        }
    }
    
    return root;
}
```
[code](C/construct-binary-search-tree-from-preorder-traversal.c)

#### Result
```
Runtime: 4 ms, faster than 62.79% of C online submissions for Construct Binary Search Tree from Preorder Traversal.
Memory Usage: 5.8 MB, less than 100.00% of C online submissions for Construct Binary Search Tree from Preorder Traversal.
```

### Python 
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def bstFromPreorder(self, preorder: List[int]) -> TreeNode:
        self.topIndex = 0;
        
        def buildTree(max = float('inf')):
            if self.topIndex >= len(preorder) or preorder[self.topIndex] > max:
                return None
            
            root = TreeNode(preorder[self.topIndex])
            self.topIndex += 1
            root.left = buildTree(root.val)
            root.right = buildTree(max)
            
            return root
        
        return buildTree()
```
[code](Python/construct-binary-search-tree-from-preorder-traversal.py)

#### Result
```
Runtime: 36 ms, faster than 62.89% of Python3 online submissions for Construct Binary Search Tree from Preorder Traversal.
Memory Usage: 14 MB, less than 6.67% of Python3 online submissions for Construct Binary Search Tree from Preorder Traversal.
```
