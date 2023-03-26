```ad-note
title: Complexidade
collapse: true

- Search: $O(h)$
- Insert: $O(h)$
- Remove: $O(h)$
- Find max/min key: $O(h)$
```

```cpp
template <typename T>
class BST {
public:
    BST() {
        this->root = nullptr;
    }

    ~BST() {
        this->free(this->root);
    }

    bool search(T v) {
        return this->search(this->root, v);
    }

    void insert(T v) {
        this->insert(this->root, v);
    }

    void remove(T v) {
        this->remove(this->root, v);
    }

    T minimun_key() {
        if (this->root == nullptr) {
            std::runtime_error("bst size == 0");
        }

        return this->minimun_key(this->root);
    }

    T maximun_key() {
        if (this->root == nullptr) {
            std::runtime_error("bst size == 0");
        }

        return this->maximun_key(this->root);
    }

    void print_inorder() {
        this->print_inorder(this->root);
    }

    void print_preorder() {
        this->print_preorder(this->root);
    }

    void print_postorder() {
        this->print_postorder(this->root);
    }

    bool empty() {
        return this->root == nullptr;
    }

private:
    struct Node {
        T key;
        Node *left;
        Node *right;

        Node(T v) {
            this->key = v;
            this->left = nullptr;
            this->right = nullptr;
        }
    };

    Node *root;

    bool search(Node *node, T v) {
        if (node == nullptr) {
            return false;
        } else if (node->key == v) {
            return true;
        }

        if (v < node->key) {
            return this->search(node->left, v);
        }

        return this->search(node->right, v);
    }

    void insert(Node *&node, T v) {
        if (node == nullptr) {
            node = new Node(v);
        }

        if (v < node->key) {
            this->insert(node->left, v);
        } else if (v > node->key) {
            this->insert(node->right, v);
        }
    }

    void remove(BST::Node *&node, T v) {
        if (node == nullptr) {
            return;
        }

        if (node->key == v) {
            if (node->left == nullptr || node->right == nullptr) {
                delete std::exchange(node, node->left != nullptr ? node->left : node->right);

                return;
            }

            node->key = this->minimun_key(node->right);

            this->remove(node->right, node->key);

            return;
        }

        if (v < node->key) {
            this->remove(node->left, v);
        } else {
            this->remove(node->right, v);
        }
    }

    T minimun_key(Node *node) {
        if (node->left == nullptr) {
            return node->key;
        }

        return this->minimun_key(node->left);
    }

    T maximun_key(Node *node) {
        if (node->right == nullptr) {
            return node->key;
        }

        return this->maximun_key(node->right);
    }

    void print_inorder(Node *node) {
        if (node == nullptr) {
            return;
        }

        this->print_inorder(node->left);

        cout << node->key << '\n';

        this->print_inorder(node->right);
    }

    void print_preorder(Node *node) {
        if (node == nullptr) {
            return;
        }

        cout << node->key << '\n';

        this->print_preorder(node->left);
        this->print_preorder(node->right);
    }

    void print_postorder(Node *node) {
        if (node == nullptr) {
            return;
        }

        this->print_postorder(node->left);
        this->print_postorder(node->right);

        cout << node->key << '\n';
    }

    void free(Node *node) {
        if (node == nullptr) {
            return;
        }

        this->free(node->left);
        this->free(node->right);

        delete node;
    }
};
```

---