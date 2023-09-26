> [!info] Objetivo
> - Organizar os dados de uma maneira em que seja possível fazer operações de inserção, remoção, etc. Basicamente para cada nó $i$ todos os filhos a esquerda de $i$ são menores e todos os filhos a direita de $i$ são maiores.

> [!note]- Complexidade
> - Search: $O(h)$
> - Insert: $O(h)$
> - Remove: $O(h)$
> - Find max/min key: $O(h)$

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

    bool search(const T &v) const {
        return this->search(this->root, v);
    }

    void insert(const T &v) {
        this->insert(this->root, v);
    }

    void remove(const T &v) {
        this->remove(this->root, v);
    }

    T minimum_key() const {
        if (this->root == nullptr) {
            runtime_error("BST size == 0");
        }

        return this->minimum_key(this->root);
    }

    T maximum_key() const {
        if (this->root == nullptr) {
            runtime_error("BST size == 0");
        }

        return this->maximum_key(this->root);
    }

    void print_inorder() const {
        this->print_inorder(this->root);
    }

    void print_preorder() const {
        this->print_preorder(this->root);
    }

    void print_postorder() const {
        this->print_postorder(this->root);
    }

    bool empty() const {
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

    bool search(const Node *node, const T &v) const {
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

    void insert(Node *&node, const T &v) {
        if (node == nullptr) {
            node = new Node(v);
        }

        if (v < node->key) {
            this->insert(node->left, v);
        } else if (v > node->key) {
            this->insert(node->right, v);
        }
    }

    void remove(Node *&node, const T &v) {
        if (node == nullptr) {
            return;
        }

        if (node->key == v) {
            if (node->left == nullptr || node->right == nullptr) {
                delete exchange(node, node->left != nullptr ? node->left : node->right);

                return;
            }

            node->key = this->minimum_key(node->right);

            this->remove(node->right, node->key);

            return;
        }

        if (v < node->key) {
            this->remove(node->left, v);
        } else {
            this->remove(node->right, v);
        }
    }

    T minimum_key(const Node *node) const {
        if (node->left == nullptr) {
            return node->key;
        }

        return this->minimum_key(node->left);
    }

    T maximum_key(const Node *node) const {
        if (node->right == nullptr) {
            return node->key;
        }

        return this->maximum_key(node->right);
    }

    void print_inorder(const Node *node) const {
        if (node == nullptr) {
            return;
        }

        this->print_inorder(node->left);

        cout << node->key << '\n';

        this->print_inorder(node->right);
    }

    void print_preorder(const Node *node) const {
        if (node == nullptr) {
            return;
        }

        cout << node->key << '\n';

        this->print_preorder(node->left);
        this->print_preorder(node->right);
    }

    void print_postorder(const Node *node) const {
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