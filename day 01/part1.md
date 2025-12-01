```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s;
    int x = 50, ans = 0;

    while (cin >> s) {
        int v = stoi(s.substr(1, 10000));

        int inc = s[0] == 'R' ? 1 : -1;
        x += v * inc;

        ans += (x % 100 == 0);
    }
    cout << ans;
}
```
