> [!info] Objetivo
> - Line sweep é uma técnica muito utilizada em várias áreas não só na geometria. Consiste basicamente em uma linha passando por um plano cartesiano seja na vertical ou na horizontal.

`````ad-example
title: Exemplo com a questão [Wifi](https://neps.academy/br/exercise/210) da OBI 2018.

> [!note]- Complexidade
> - $O(n \log n)$

```cpp
#include <bits/stdc++.h>

using namespace std;

typedef pair<int, int> pii;

struct Event {
    int x;
    int l;
    int r;
    int type;

    Event(int x, int l, int r, int type) {
        this->x = x;
        this->l = l;
        this->r = r;
        this->type = type;
    }

    bool operator<(const Event &other) const {
        if (this->x != other.x) {
            return this->x < other.x;
        }

        return this->type < other.type;
    }
};

int main() {
    int n;

    cin >> n;

    vector<Event> events;

    for (int i {}; i < n; ++i) {
        int x1, y1, x2, y2;

        cin >> x1 >> y1 >> x2 >> y2;

        events.emplace_back(x1, y2, y1, 1);
        events.emplace_back(x2, y2, y1, 2);
    }

    sort(events.begin(), events.end());

    set<pii> current_events;

    int ans {};

    for (const auto [x, l, r, type] : events) {
        if (type == 1) {
            set<pii>::iterator it {current_events.upper_bound({r, 0})};

            while (it != current_events.end()) {
                if (it->first > r && it->second < l) {
                    it = current_events.erase(it);
                } else {
                    break;
                }
            }

            current_events.insert({r, l});
        } else {
            size_t erased_count {current_events.erase({r, l})};

            if (erased_count != 0) {
                ++ans;
            }
        }
    }

    cout << ans << '\n';

    return 0;
}
```
`````

---