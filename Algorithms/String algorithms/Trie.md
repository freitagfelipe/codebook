> [!info] Objetivo
> - Tem como objetivo armazenar e buscar palavras, nessa estrutura cada nó da árvore representa um caractere e o caminho até uma folha é formado pelos prefixos da palavra.

> [!note]- Complexidade
> - Add/remove/exists: $O(n)$
> - Count prefix/string: $O(n)$

```cpp
class Trie {
public:
    Trie() {
        this->trie.emplace_back();
    }

    void add(const string &s) {
        int v {};

        for (char ch : s) {
            ++this->trie[v].count;
            
            int c {this->get_id(ch)};

            if (this->trie[v].next[c] == -1) {
                this->trie[v].next[c] = this->trie.size();
                this->trie.emplace_back();
            }

            v = this->trie[v].next[c];
        }

        ++this->trie[v].leaf;
    }

    bool exists(const string &s) {
        int v {};

        for (char ch : s) {
            int c {this->get_id(ch)};

            if (this->trie[v].next[c] == -1) {
                return false;
            }
        }

        return this->trie[v].leaf > 0;
    }

    int count_str(const string &s) {
        int v {};

        for (int ch : s) {
            int c {this->get_id(ch)};

            if (this->trie[v].next[c] == -1) {
                return 0;
            }

            v = this->trie[v].next[c];
        }

        return this->trie[v].leaf;
    }

    int count_pre(const string &s) {
        int v {};

        for (int ch : s) {
            int c {this->get_id(ch)};

            if (this->trie[v].next[c] == -1) {
                return 0;
            }

            v = this->trie[v].next[c];
        }

        return this->trie[v].count;
    }

    bool remove(const string &s) {
        vector<int> rm;
        int v {};

        for (char ch : s) {
            rm.push_back(v);

            int c {this->get_id(ch)};

            if (this->trie[v].next[c] == -1) {
                return false;
            }

            v = this->trie[v].next[c];
        }

        if (this->trie[v].leaf != 0) {
            --this->trie[v].leaf;

            for (int x : rm) {
                --this->trie[x].count;
            }

            return true;
        }

        return false;
    }

private:
    static const int ALPHABETE_SIZE = 26;

    struct Node {
        int next[Trie::ALPHABETE_SIZE];
        int leaf;
        int count;

        Node() {
            fill(begin(next), end(next), -1);

            this->leaf = 0;
            this->count = 0;
        }
    };

    vector<Node> trie;

    int get_id(char c) {
        return c - 'a';
    }
};
```

---