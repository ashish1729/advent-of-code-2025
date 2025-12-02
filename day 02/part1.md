```cpp
#include <bits/stdc++.h>
using namespace std;

vector<string> split(string& s, char sep = ' ') {
    string curr = ""; vector<string> ans;
    for (char c : s) {
        if (c == sep) { ans.push_back(curr); curr = ""; }
        else { curr += c; }
    }
    ans.push_back(curr);
    return ans;
}

int main() {
    string line; cin >> line;
    vector<string> ar = split(line, ',');

    vector<long long> invalid; invalid.reserve(1e7);

    for (int i = 1; i < 1e5; i++) {
        string s = to_string(i);
        s = s + s;

        invalid.push_back(stoll(s));
    }

    long long ans = 0;

    for (auto& s : ar) {
        vector<string> parts = split(s, '-');
        long long l = stoll(parts[0]);
        long long r = stoll(parts[1]);

        for (auto& id : invalid) if (id >= l and id <= r) ans += id;
    }

    cout << ans;
}
```
