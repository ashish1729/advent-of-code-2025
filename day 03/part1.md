```cpp
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp> // Common file
#include <ext/pb_ds/tree_policy.hpp> // Including tree_order_statistics_node_update

using namespace std;
using namespace __gnu_pbds;
template <typename T>
using ordered_set = tree<T, null_type, less<T>, rb_tree_tag, tree_order_statistics_node_update>;

typedef bool boolean;
typedef long long ll;
typedef pair<int, int> ii;
typedef vector<int> vi;
typedef vector<bool> vb;
typedef vector<vb> vvb;
typedef vector<long long> vl;
typedef vector<pair<int, int>> vii;
typedef vector<vector<pair<int, int>>> vvii;
typedef vector<string> vs;
typedef vector<vs> vvs;
typedef vector<vector<int>> vvi;
typedef vector<vector<long long>> vvl;
typedef vector<vector<pair<int, long long>>> vvil;
typedef tuple<int, int, int> iii;

string nl = "\n";
string sp = " ";

#define IGNORE_REMAINING_LINE cin.ignore(numeric_limits<streamsize>::max(), '\n')

#define has(cnt, key) (((cnt).find((key))) != ((cnt).end()))
#define isOdd(x) (((x) & 1) == 1)
#define isEven(x) (not(isOdd(x)))
#define all(x) (x).begin(), (x).end()
#define maxim(x) (*max_element((x).begin(), ((x).end())))
#define minim(x) (*min_element((x).begin(), ((x).end())))
#define smax(a, b) (a) = max((a), (b))
#define smin(a, b) (a) = min((a), (b))
#define sz(x) ((int)((x).size()))
#define len(x) ((int)((x).size()))
#define glen(x,y) int y = ((int)((x).size()))
#define srt(x) sort((x).begin(), (x).end())
#define srtr(x) sort((x).rbegin(), (x).rend())
#define rev(x) reverse((x).begin(), (x).end())
#define pb push_back
#define gcd(x,y) (__gcd((x),(y)))
#define lcm(x,y) ((ll)(x) / gcd((x),(y)) * (y))
#define bitcount(x) __builtin_popcountll(x)
#define inGrid(a,b,r,c) ((a) >= 0 and (a) < (r) and (b) >= 0 and (b) < (c))
#define ceilDiv(a,b) (((a) +(b) - 1) / (b))

#define no cout << "NO" << nl
#define yes cout << "YES" << nl
#define yn(p) if((p)) yes; else no;

#define elif else if
#define FOR(i, s, e) for (int i = (s); i < (e); ++i)
#define fori(i, s, e) for (int i = (s); i <= (e); ++i)
#define forr(i, e, s) for (int i = (e); i > (s); --i)
#define forri(i, e, s) for (int i = (e); i >= (s); --i)
#define rep(n) for (int i = 0; i < (n); ++i)
#define til(i, n) for (int i = 0; i < (n); ++i)
#define iter(cntr) for (auto &x : (cntr))
#define iterv(val,cntr) for(auto &val: (cntr))
#define enmrt(cntr) for(int i = 0, auto x = ((cntr)[0]); i < sz((cntr)); ++i, x = ((cntr)[i]) )

vector<string> split(string& s, char sep = ' ') {
    string curr = ""; vector<string> ans;
    for (char c : s) {
        if (c == sep) { ans.push_back(curr); curr = ""; }
        else { curr += c; }
    }
    ans.push_back(curr);
    return ans;
}
// Input stuff

#define ri(x) int x; cin >> x;
#define rl(x) long long x; cin >> x;
#define rs(x) string x; cin >> x
#define ria(cntnr,n) vector<int> cntnr(n);for (int &x : cntnr) cin >> x;
#define rla(cntnr, n) vector<long long> cntnr(n); for (long long &x : cntnr)cin >> x;
#define rsa(cntnr, n) vector<string> cntnr(n);for (string & x : cntnr)  cin >> x;

// Output stuff
#define pv(cntnr) {for (auto &xx : cntnr) cout << xx << " "; cout << "\n";}

void dbg_out() { cout << "\n"; }
template<typename H, typename... T>
void dbg_out(H head, T... tail) { cout << head << " "; dbg_out(tail...); }
#define dbg(...)  dbg_out(__VA_ARGS__)
#define dbgx(...) cout << "{" << #__VA_ARGS__ << "}:", dbg_out(__VA_ARGS__)

// these are clockwise
vector<vector<int>> eightDirections = {
     {-1, 0}, {-1, 1}, {0, 1}, {1, 1}, {1, 0},  {1, -1} , {0, -1},{-1, -1} };
vector<vector<int>> fourDirections = { {-1, 0}, {0, 1}, {1, 0}, {0, -1} };
vector<vector<int>> diagonalDirections = { {-1, -1}, {-1, 1}, {1, 1}, {1, -1} };
vector<vector<int>> knightMoves{ {1, 2}, {1, -2}, {-1, 2}, {-1, -2}, {2, 1}, {2, -1}, {-2, 1}, {-2, -1} };
// add debuggin section

/*
// code to measure execution time
// https://stackoverflow.com/questions/876901/calculating-execution-time-in-c
auto start = std::chrono::steady_clock::now();

auto end = std::chrono::steady_clock::now();
auto diff = end - start;
// milliseconds
std::cout << std::chrono::duration<double, std::milli>(diff).count() << " ms" << std::endl;
// nanoseconds
std::cout << std::chrono::duration<double, std::nano>(diff).count() << " ns" << std::endl;
*/

void preprocess();
void solve(int testCaseNumber);

bool _CHECKED_MULTIPLE_TEST_CASES = false;
int _TOTAL_NUMBER_OF_CASES = 1;
bool _PRINT_GAP_BETWEEN_CASES = false;

void multipleTestCase(bool hasGapBetweenCases = false) {
    if (_CHECKED_MULTIPLE_TEST_CASES) return;
    _CHECKED_MULTIPLE_TEST_CASES = true;
    _PRINT_GAP_BETWEEN_CASES = hasGapBetweenCases;

    cin >> _TOTAL_NUMBER_OF_CASES;
}

int32_t main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    cout << fixed << setprecision(15);
    preprocess();

    for (int i = 1; i <= _TOTAL_NUMBER_OF_CASES; i++) {
        if (_PRINT_GAP_BETWEEN_CASES) cout << nl;
        solve(i);
    }
    return 0;
}
// ---- code below this -----


void solve(int TC) {
    int ans = 0; string s;
    while (cin >> s) {
        int n = len(s), val = 0;
        til(i, n) til(j, i) smax(val, 10 * (s[j] - '0') + (s[i] - '0'));
        ans += val;
    }
    dbg(ans);
}

void preprocess() {}
```
