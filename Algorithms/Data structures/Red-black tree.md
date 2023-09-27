> [!info] Objetivo
> - A árvore rubro negra implementa a mesma ideia da [[Binary search tree (BST)]] só que ela é balanceada, fazendo com que as consultas na estrutura sejam bem rápidas.

> [!caution] Restrições da estrutura
> - Cada nó tem uma cor: vermelho ou preto.
> - A cor da raiz é preto.
> - Não há nós vermelhos adjacentes.
> - Cada caminho desde um nó até qualquer um dos seus descendentes $NULL$ tem o mesmo número de nós pretos.

> [!note]- Complexidade
> - Search/insert/remove: $O(\log n)$
> - Find min/max key: $O(\log n)$

```cpp
template <typename T>
class RedBlackTree {
public:
    RedBlackTree() {
        this->null = new Node();

        this->null->left = this->null->right = this->null->parent = this->null;

        this->root = this->null;
    }

    ~RedBlackTree() {
        delete this->null;

        this->free(this->root);
    }

    bool search(const T &x) const {
        return this->search(this->root, x);
    }

    void insert(const T &x) {
        if (this->search(x)) {
            return;
        }

        Node *new_node {this->create_node(x, Node::Color::RED)};

        this->insert(this->root, this->null, new_node);

        this->fix_insertion(new_node);
    }

    void remove(const T &x) {
        if (!this->search(x)) {
            return;
        }

        Node *node {nullptr};

        this->remove(this->root, x, this->null, node);

        this->fix_deletion(node);
    }

    T minimum_key() const {
        if (this->root == this->null) {
            runtime_error("Red black tree size == 0");
        }

        return this->minimum_key(this->root);
    }

    T maximum_key() const {
        if (this->root == this->null) {
            runtime_error("Red black tree size == 0");
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
        return this->root == this->null;
    }

public:
    struct Node {
        enum class Color { BLACK, RED, BOLD };

        T key;
        Node::Color color;
        Node *left {nullptr};
        Node *right {nullptr};
        Node *parent {nullptr};

        Node() {
            this->key = {};
            this->color = Node::Color::BLACK;
        }

        Node(T key, Color color) {
            this->key = key;
            this->color = color;
        }

        bool is_left_child() {
            return this->parent->left == this;
        }

        Node *grandparent() {
            if (this->parent == nullptr) {
                runtime_error("Call grandparent but parent is nullptr");
            }

            return this->parent->parent;
        }

        Node *sibling() {
            if (this->parent == nullptr) {
                runtime_error("Call grandparent but parent is nullptr");
            }

            if (this->is_left_child()) {
                return this->parent->right;
            }

            return this->parent->left;
        }

        Node *uncle() {
            if (this->parent == nullptr) {
                runtime_error("Call grandparent but parent is nullptr");
            }

            return this->parent->sibling();
        }

        static Node::Color merge_colors(const Node::Color a, const Node::Color b) {
            if (a == Node::Color::RED && b == Node::Color::RED) {
                return Node::Color::RED;
            }

            if (a == Node::Color::BLACK && b == Node::Color::BLACK) {
                return Node::Color::BOLD;
            }

            return Node::Color::BLACK;
        }
    };

    Node *root;
    Node *null;

    Node *create_node(const T &key, const typename Node::Color color) {
        Node *node {new Node(key, color)};

        node->left = node->right = node->parent = this->null;

        return node;
    }

    bool search(const Node *node, const T &x) const {
        if (node == this->null) {
            return false;
        } else if (node->key == x) {
            return true;
        }

        if (node->key > x) {
            return this->search(node->left, x);
        }

        return this->search(node->right, x);
    }

    void insert(Node *&node, Node *parent, Node *new_node) {
        if (node == this->null) {
            new_node->parent = parent;

            node = new_node;

            return;
        }

        if (node->key > new_node->key) {
            this->insert(node->left, node, new_node);
        } else if (node->key < new_node->key) {
            this->insert(node->right, node, new_node);
        }
    }

    void remove(Node *&node, const T &x, Node *parent, Node *&may_need_fix) {
        if (node->key == x) {
            if (node->left == this->null || node->right == this->null) {
                typename Node::Color old_color {node->color};

                delete exchange(node, node->left != this->null ? node->left : node->right);

                node->parent = parent;

                node->color = Node::merge_colors(node->color, old_color);

                may_need_fix = node;
            } else {
                node->key = this->minimum_key(node->right);

                this->remove(node->right, node->key, node, may_need_fix);
            }

            return;
        }

        if (node->key > x) {
            this->remove(node->left, x, node, may_need_fix);
        } else {
            this->remove(node->right, x, node, may_need_fix);
        }
    }

    T minimum_key(const Node *node) const {
        if (node->left == this->null) {
            return node->key;
        }

        return this->minimum_key(node->left);
    }

    T maximum_key(const Node *node) const {
        if (node->right == this->null) {
            return node->key;
        }

        return this->maximum_key(node->right);
    }

    void print_inorder(const Node *node) const {
        if (node == this->null) {
            return;
        }

        this->print_inorder(node->left);

        cout << node->key << '\n';

        this->print_inorder(node->right);
    }

    void print_preorder(const Node *node) const {
        if (node == this->null) {
            return;
        }

        cout << node->key << '\n';

        this->print_preorder(node->left);
        this->print_preorder(node->right);
    }

    void print_postorder(const Node *node) const {
        if (node == this->null) {
            return;
        }

        this->print_postorder(node->left);
        this->print_postorder(node->right);

        cout << node->key << '\n';
    }

    void left_rotation(Node *node) {
        Node *x {node->right};
        Node *beta {x->left};

        node->right = beta;

        if (beta != this->null) {
            beta->parent = node;
        }

        x->parent = node->parent;

        if (node->parent == this->null) {
            this->root = x;
        } else if (node->is_left_child()) {
            node->parent->left = x;
        } else {
            node->parent->right = x;
        }

        x->left = node;
        node->parent = x;
    }

    void right_rotation(Node *node) {
        Node *x {node->left};
        Node *beta {x->right};

        node->left = beta;

        if (beta != this->null) {
            beta->parent = node;
        }

        x->parent = node->parent;

        if (node->parent == this->null) {
            this->root = x;
        } else if (node->is_left_child()) {
            node->parent->left = x;
        } else {
            node->parent->right = x;
        }

        x->right = node;
        node->parent = x;
    }

    void fix_insertion(Node *node) {
        if (node == this->root) {
            node->color = Node::Color::BLACK;

            return;
        }

        Node *g {node->grandparent()};
        Node *p {node->parent};
        Node *u {node->uncle()};

        if (p->color == Node::Color::BLACK) {
            return;
        }

        if (u->color == Node::Color::RED) {
            g->color = Node::Color::RED;
            p->color = u->color = Node::Color::BLACK;

            this->fix_insertion(g);

            return;
        }

        if (node->is_left_child() == p->is_left_child()) {
            p->color = Node::Color::BLACK;
            g->color = Node::Color::RED;

            if (node->is_left_child()) {
                this->right_rotation(g);
            } else {
                this->left_rotation(g);
            }

            return;
        }

        if (p->is_left_child()) {
            this->left_rotation(p);
        } else {
            this->right_rotation(p);
        }

        this->fix_insertion(p);
    }

    typename Node::Color check_color(Node *node) {
        if (node == this->null) {
            return Node::Color::BLACK;
        }

        return node->color;
    }

    void fix_deletion(Node *node) {
        if (node->color != Node::Color::BOLD) {
            return;
        }

        if (node == this->root) {
            node->color = Node::Color::BLACK;

            return;
        }

        Node *p {node->parent};
        Node *s {node->sibling()};
        Node *l {s->left};
        Node *r {s->right};

        if (this->check_color(s) == Node::Color::RED) {
            s->color = Node::Color::BLACK;
            p->color = Node::Color::RED;

            if (node->is_left_child()) {
                this->left_rotation(p);
            } else {
                this->right_rotation(p);
            }

            this->fix_deletion(node);

            return;
        }

        if (this->check_color(l) == Node::Color::BLACK && this->check_color(r) == Node::Color::BLACK) {
            node->color = Node::Color::BLACK;
            s->color = Node::Color::RED;
            p->color = Node::merge_colors(p->color, Node::Color::BLACK);

            this->fix_deletion(p);

            return;
        }

        if (node->is_left_child()) {
            if (this->check_color(l) == Node::Color::RED && this->check_color(r) == Node::Color::BLACK) {
                s->color = Node::Color::RED;
                l->color = Node::Color::BLACK;

                this->right_rotation(s);

                this->fix_deletion(node);

                return;
            }

            s->color = p->color;
            p->color = r->color = node->color = Node::Color::BLACK;

            this->left_rotation(p);
        } else {
            if (this->check_color(l) == Node::Color::BLACK && this->check_color(r) == Node::Color::RED) {
                s->color = Node::Color::RED;
                r->color = Node::Color::BLACK;

                this->left_rotation(s);

                this->fix_deletion(node);

                return;
            }

            s->color = p->color;
            p->color = l->color = node->color = Node::Color::BLACK;

            this->right_rotation(p);
        }
    }

    void free(Node *node) {
        if (node == this->null) {
            return;
        }

        this->free(node->left);
        this->free(node->right);

        delete node;
    }
};
```

---