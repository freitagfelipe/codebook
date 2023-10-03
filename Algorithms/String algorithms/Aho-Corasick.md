> [!info] Objetivo
> - Permite pesquisarmos de forma rápida vários padrões de uma só vez em um texto. É construído um autômato em cima de uma [[Trie]] que consiste de transições feitas com suffix links.

> [!note]- Complexidade
> - Insert: $O(n)$
> - Match amount: $O(n)$

```cpp
typedef long long ll;

class AhoCorasick {
public:
    AhoCorasick() {
        this->trie.emplace_back();
    }

    void add(const string &s) {
        int v {};

        for (char ch : s) {
            int c {this->get_id(ch)};

            if (this->trie[v].next[c] == -1) {
                this->trie[v].next[c] = this->trie.size();
                this->trie.emplace_back(v, ch);
            }

            v = this->trie[v].next[c];
        }

        this->trie[v].leaf = true;
    }

    ll match_amount(const string &t) {
        int v {};
        ll ans {};
        
        for (char ch : t) {
            v = this->go(v, ch);

            ans += this->count_match(v);
        }

        return ans;
    }

private:
    static const int ALPHABETE_SIZE = 26;

    struct Node {
        int next[AhoCorasick::ALPHABETE_SIZE];
        int go[AhoCorasick::ALPHABETE_SIZE];
        bool leaf;
        int p;
        char pch;
        int suff_link;
        int end_link;
        int match;

        Node(int p = -1, char ch = '$') {
            fill(begin(next), end(next), -1);
            fill(begin(go), end(go), -1);

            this->leaf = false;
            this->p = p;
            this->pch = ch;
            this->suff_link = -1;
            this->end_link = -1;
            this->match = -1;
        }
    };

    vector<Node> trie;

    int get_id(char c) {
        return c - 'a';
    }

    int go(int v, char ch) {
        int c {get_id(ch)};

        if (this->trie[v].go[c] == -1) {
            if (this->trie[v].next[c] != -1) {
                this->trie[v].go[c] = this->trie[v].next[c];
            } else {
                this->trie[v].go[c] = v == 0 ? 0 : this->go(this->get_suff_link(v), ch);
            }
        }

        return this->trie[v].go[c];
    }

    int get_suff_link(int v) {
        if (this->trie[v].suff_link == -1) {
            if (v == 0 || this->trie[v].p == 0) {
                this->trie[v].suff_link = 0;
            } else {
                this->trie[v].suff_link = this->go(this->get_suff_link(this->trie[v].p), this->trie[v].pch);
            }
        }

        return this->trie[v].suff_link;
    }

    int get_end_link(int v) {
        if (this->trie[v].end_link == -1) {
            if (v == 0 || this->trie[v].p == 0) {
                this->trie[v].end_link = 0;
            } else {
                int suff_link {this->get_suff_link(v)};

                if (this->trie[suff_link].leaf) {
                    this->trie[v].end_link = suff_link;
                } else {
                    this->trie[v].end_link = this->get_end_link(suff_link);
                }
            }
        }

        return this->trie[v].end_link;
    }

    int count_match(int v) {
        if (this->trie[v].match == -1) {
            if (v == 0 || this->trie[v].p == 0) {
			    this->trie[v].match = this->trie[v].leaf;
            } else {
		        this->trie[v].match = this->trie[v].leaf + this->count_match(this->get_end_link(v));
            }
        }

        return this->trie[v].match;
    }
};
```

---