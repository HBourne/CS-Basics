#### LRU
```
class LRUCache {
private:
    unordered_map<int, list<pair<int, int>>::iterator> d;
    list<pair<int, int>> l;
    int c;
    
public:
    LRUCache(int capacity) {
        c = capacity;
    }
    
    int get(int key) {
        if (d.find(key) == d.end()) return -1;
        put(key, d[key]->second);
        return d[key]->second;
    }
    
    void put(int key, int value) {
        if (d.find(key) != d.end()) {
            l.erase(d[key]);
        }
        if (l.size() == c) {
            d.erase(l.front().first);
            l.pop_front();
        }
        l.push_back(make_pair(key, value));
        d[key] = --l.end();
    }
};
```

#### Construct Binary Tree from Preorder and Inorder Traversal
```
TreeNode* helper(vector<int>& preorder, int pl, int pr, vector<int>& inorder, int il, int ir) {
    if (pl >= pr) return nullptr;
    TreeNode* root = new TreeNode(preorder[pl]);
    auto loc = find(inorder.begin() + il, inorder.begin() + ir, preorder[pl]);
    int dis = loc - inorder.begin() - il;
    root->left = helper(preorder, pl + 1, pl + 1 + dis, inorder, il, il + dis);
    root->right = helper(preorder, pl + 1 + dis, pr, inorder, il + dis + 1, ir);
    return root;
}

TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
    return helper(preorder, 0, preorder.size(), inorder, 0, inorder.size());
}
```

#### Recover Binary Search Tree
```
void recoverTree(TreeNode* root) {
    TreeNode* f1 = nullptr, * f2 = nullptr, * prev = nullptr;
    stack<TreeNode*> s;
    while (!s.empty() || root) {
        while (root != nullptr) {
            s.push(root);
            root = root->left;
        }
        root = s.top();
        s.pop();
        if (prev != nullptr) {
            if (prev->val >= root->val) {
                if (f1 == nullptr) {
                    f1 = prev;
                    f2 = root;
                } else {
                    f2 = root;
                    swap(f1->val, f2->val);
                    return;
                }
            }
        }
        prev = root;
        root = root->right;
    }
    swap(f1->val, f2->val);
}
```