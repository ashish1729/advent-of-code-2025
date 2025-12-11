- not a general solution but hacky to work for my input
- in the end there is `p5.js` snippet which plots the polygon for my cases
    - the cordinates in that code are compressed
- I made few assumptions
    - valid rect will be inside polygon and it will not have any red inside the boundary (on boundary is OK)
    - second assumption is largest rect will not cross that line in between ( see the plot )


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

#define no cout << "No" << nl
#define yes cout << "Yes" << nl
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


double EPS = 1e-9;
struct point {
    double x, y;
    point() { x = y = 0; };
    point(double a, double b) { x = a; y = b; }

    bool operator < (point other) const {
        if (fabs(x - other.x) > EPS) return x < other.x;
        return y < other.y;
    }

    bool operator == (point other) const {
        return fabs(x - other.x) < EPS and fabs(y - other.y) < EPS;
    }
};

double dist(point a, point b) {
    return hypot(a.x - b.x, a.y - b.y);
}

double DEG_to_RAD(double deg) { return deg * M_PI / 180; }
double RAD_to_DEG(double rad) { return rad * 180 / M_PI; }

// rotate a point around origin
point rotate(const point& p, double angleInDegrees) {
    double rad = DEG_to_RAD(angleInDegrees);
    return point(p.x * cos(rad) - p.y * sin(rad), p.x * sin(rad) + p.y * cos(rad));
}


struct line { // b is either 0.0 ( for vertical lines ) or 1.0
    double a, b, c; // general form `ax + by + c = 0`
};

line pointsToLine(const point& p, const point& q) {
    if (fabs(p.x - q.x) < EPS) return { 1, 0, -p.x }; // b = 0 for vertical
    double a = -(p.y - q.y) / (p.x - q.x);
    return { a, 1, -p.x * a - p.y }; // b = 1 for non vertical
}

line pointSlopeToLine(point& p, double slope) { // slope is not infinity 
    return { -slope, 1.0, slope * p.x - p.y };
}

bool areParallel(line& g, line& h) {
    return fabs(g.a - h.a) < EPS and fabs(g.b - h.b) < EPS;
}

bool areSame(line& g, line& h) {
    return fabs(g.a - h.a) < EPS and fabs(g.b - h.b) < EPS and fabs(g.c - h.c) < EPS;
}

pair<bool, point> findIntersection(line& g, line& h) {
    if (areSame(g, h)) return { true, {0, -g.c} }; // there are infinite points, I return 1
    if (areParallel(g, h)) return { false, {} };
    double x = -(g.b * h.c - g.c * h.b) / (g.b * h.a - g.a * h.b);
    double y;
    // this y formula has /b in the end but our b will be 1.0 if not zero
    if (fabs(g.b) > 0) y = -(g.a * x + g.c);
    else y = -(h.a * x + h.c);

    return { true, {x,y} };
}


struct vec {
    double x; double y;
    vec(double _x, double _y) { x = _x; y = _y; }
};

vec toVec(const point& a, const point& b) {
    return vec(b.x - a.x, b.y - a.y);
}

vec scale(const vec& v, double factor) {
    return vec(v.x * factor, v.y * factor);
}

point translate(const point& p, const vec& v) {
    return point(p.x + v.x, p.y + v.y);
}

double dot(const vec& a, const vec& b) {
    return a.x * b.x + a.y * b.y;
}

double magnitude_square(const vec& a) {
    return a.x * a.x + a.y * a.y;
}

double angle(const point& a, const point& o, const point& b) { // return angle aob
    vec oa = toVec(o, a), ob = toVec(o, b);
    return acos(dot(oa, ob) / sqrt(magnitude_square(oa) * magnitude_square(ob)));
}

double cross(const vec& a, const vec& b) {
    return a.x * b.y - a.y * b.x;
}

bool isCounterClockWise(const point& p, const point& q, const point& r) {
    // does going from p-q-r make counterclockwise/left turn
    return cross(toVec(p, q), toVec(p, r)) > EPS;
}

bool areCollinear(const point& p, const point& q, const point& r) {
    return fabs(cross(toVec(p, q), toVec(p, r))) < EPS;
}

pair<double, point> distanceToLine(const point& p, const point& a, const point& b) {
    // distance of point `p`, from line passing through `a` and `b`
    // returns distance and point on line which is closest to p 
    vec ap = toVec(a, p), ab = toVec(a, b);
    double u = dot(ap, ab) / magnitude_square(ab);
    point c = translate(a, scale(ab, u));
    return { dist(c,p), c };
}

pair<double, point> distanceToLineSegment(const point& p, const point& a, const point& b) {
    // distance of point `p`, from line segment ending at `a` and `b`
    // returns distance and point on line segment which is closest to p 
    vec ap = toVec(a, p), ab = toVec(a, b);
    double u = dot(ap, ab) / magnitude_square(ab);
    point c;
    if (u < 0)  c = point(a.x, a.y);
    else if (u > 0)  c = point(b.x, b.y);
    else c = translate(a, scale(ab, u));

    return { dist(c,p), c };
}


// polygons

double perimeter(const vector<point>& poly) {
    double ans = 0;
    for (int i = 0; i < (int)poly.size() - 1; ++i) ans += dist(poly[i], poly[i + 1]);
    return ans;
}

double area(const vector<point>& poly) {
    double ans = 0;
    for (int i = 0; i < (int)poly.size() - 1; ++i) { // shoelace formula
        ans += poly[i].x * poly[i + 1].y - poly[i + 1].x * poly[i].y;
    }
    return fabs(ans) / 2;
}

bool isConvex(const vector<point>& poly) { // doesn't handle collinear I guess
    int n = poly.size();
    if (n <= 3) return false; // definition
    bool firstTurn = isCounterClockWise(poly[0], poly[1], poly[2]);
    for (int i = 0; i < n - 1; ++i) { // we check all turns to be in same direction
        bool currTurn = isCounterClockWise(poly[i], poly[i + 1], poly[(i + 2) == n ? 1 : i + 2]);
        if (currTurn != firstTurn) return false;
    }
    return true;
}

// returns -1 / 0 / 1 - for outside, on boundary, inside
int isInsidePolygon(const point& p, const vector<point>& poly) {
    int n = (int)poly.size();
    if (n <= 3) return -1;

    for (int i = 0; i < n - 1; ++i) {
        if (fabs(dist(poly[i], p) + dist(p, poly[i + 1]) - dist(poly[i], poly[i + 1])) < EPS) {
            return 0; // on the boundary
        }
    }

    double signedAngleSum = 0;
    for (int i = 0; i < n - 1; ++i) {
        if (isCounterClockWise(p, poly[i], poly[i + 1]))
            signedAngleSum += angle(poly[i], p, poly[i + 1]);
        else
            signedAngleSum -= angle(poly[i], p, poly[i + 1]);

    }
    // we need 2 * PI for inside and 0 for outside.. are checking with PI
    return fabs(signedAngleSum) > M_PI ? 1 : -1;
}

void solve(int TC) {
    string line;
    vector<pair<ll, ll>> ar;
    int maxi = -1;
    int id = -1;
    while (cin >> line) {
        vs a = split(line, ',');
        ar.pb({ stoll(a[0]), stoll(a[1]) });
    }
    glen(ar, n);

    til(i, n - 1) {
        if (abs(ar[i + 1].first - ar[i].first) > maxi) {
            maxi = abs(ar[i + 1].first - ar[i].first);
            id = i;
        }
    }

    dbgx(id, ar[id].second);


    vector<point> poly;
    iter(ar) poly.pb({ x.first, x.second });
    poly.pb({ ar[0].first, ar[0].second });

    ll ans = 0;

    til(i, n) til(j, i) {
        // rectangle
        int x1 = min(ar[i].first, ar[j].first);
        int x2 = max(ar[i].first, ar[j].first);
        int y1 = min(ar[i].second, ar[j].second);
        int y2 = max(ar[i].second, ar[j].second);

        // dbg("check", i, j, "->", x1, y1, "-", x2, y2);

        // bottom left
        if (isInsidePolygon({ x1,y1 }, poly) == -1) {
            // dbg("fails bottom left", x1, y1);
            continue;
        }
        // bottom right
        if (isInsidePolygon({ x2,y1 }, poly) == -1) {
            // dbg("fails bottom right", x2, y1);
            continue;
        }
        // top left
        if (isInsidePolygon({ x1,y2 }, poly) == -1) {
            // dbg("fails top left", x1, y2);
            continue;
        }
        // top right
        if (isInsidePolygon({ x2,y2 }, poly) == -1) {
            // dbg("fails top right", x2, y2);
            continue;
        }

        // dbg("here");

        bool valid = true;
        til(k, n) {
            int x = ar[k].first;
            int y = ar[k].second;

            bool inside = x > x1 and x < x2 and y > y1 and y < y2;
            if (inside) {
                valid = false;
                break;
            }
        }
        if (valid) {
            // dbg("valid");
            ll dx = abs(ar[i].first - ar[j].first) + 1;
            ll dy = abs(ar[i].second - ar[j].second) + 1;
            if (y1 < 50327 and y2 > 50327) continue;;
            ll area = dx * dy;
            if (area == 1529675217) {
                dbg(i, j, x1, y1, x2, y2);
            }
            smax(ans, area);
        }

    }

    dbg(ans);

}

void preprocess() {}



// 4650952673 - high

/*


  let mul = 3

function setup() {

  const br = [[1,0],[3,0],[3,3],[2,3],[2,2],[0,2],[0,1],[1,1],]
;
  const ar = [[244,124],[244,126],[247,126],[247,128],[241,128],[241,130],[245,130],[245,132],[243,132],[243,134],[236,134],[236,136],[232,136],[232,138],[229,138],[229,140],[235,140],[235,142],[227,142],[227,144],[226,144],[226,146],[225,146],[225,148],[222,148],[222,150],[220,150],[220,152],[219,152],[219,154],[215,154],[215,156],[214,156],[214,158],[210,158],[210,160],[211,160],[211,162],[207,162],[207,164],[206,164],[206,166],[205,166],[205,168],[202,168],[202,170],[199,170],[199,172],[198,172],[198,174],[196,174],[196,176],[193,176],[193,179],[192,179],[192,180],[190,180],[190,182],[188,182],[188,184],[186,184],[186,186],[184,186],[184,188],[182,188],[182,190],[180,190],[180,192],[178,192],[178,194],[176,194],[176,196],[174,196],[174,199],[172,199],[172,200],[170,200],[170,202],[168,202],[168,204],[166,204],[166,207],[164,207],[164,210],[162,210],[162,209],[160,209],[160,213],[158,213],[158,216],[156,216],[156,215],[154,215],[154,217],[152,217],[152,220],[150,220],[150,223],[148,223],[148,225],[146,225],[146,226],[144,226],[144,227],[142,227],[142,229],[140,229],[140,231],[138,231],[138,232],[136,232],[136,241],[134,241],[134,239],[132,239],[132,234],[130,234],[130,240],[128,240],[128,243],[126,243],[126,246],[124,246],[124,245],[122,245],[122,247],[120,247],[120,242],[118,242],[118,244],[116,244],[116,235],[114,235],[114,237],[112,237],[112,233],[110,233],[110,236],[108,236],[108,238],[106,238],[106,228],[104,228],[104,230],[102,230],[102,222],[100,222],[100,224],[98,224],[98,221],[96,221],[96,219],[94,219],[94,218],[92,218],[92,214],[90,214],[90,212],[88,212],[88,211],[86,211],[86,208],[84,208],[84,206],[82,206],[82,205],[80,205],[80,203],[78,203],[78,201],[76,201],[76,198],[74,198],[74,197],[72,197],[72,195],[70,195],[70,193],[68,193],[68,191],[66,191],[66,189],[63,189],[63,187],[62,187],[62,185],[60,185],[60,183],[58,183],[58,181],[56,181],[56,178],[54,178],[54,177],[52,177],[52,175],[50,175],[50,173],[49,173],[49,171],[46,171],[46,169],[45,169],[45,167],[41,167],[41,165],[39,165],[39,163],[38,163],[38,161],[37,161],[37,159],[34,159],[34,157],[30,157],[30,155],[32,155],[32,153],[29,153],[29,151],[26,151],[26,149],[25,149],[25,147],[22,147],[22,145],[20,145],[20,143],[19,143],[19,141],[13,141],[13,139],[14,139],[14,137],[15,137],[15,135],[8,135],[8,133],[5,133],[5,131],[2,131],[2,129],[0,129],[0,127],[9,127],[9,125],[7,125],[7,123],[218,123],[218,121],[10,121],[10,119],[4,119],[4,117],[3,117],[3,115],[1,115],[1,113],[6,113],[6,111],[11,111],[11,109],[12,109],[12,107],[16,107],[16,105],[17,105],[17,103],[21,103],[21,101],[18,101],[18,99],[24,99],[24,97],[23,97],[23,95],[28,95],[28,93],[27,93],[27,91],[31,91],[31,89],[33,89],[33,87],[35,87],[35,85],[36,85],[36,83],[40,83],[40,81],[42,81],[42,79],[44,79],[44,77],[43,77],[43,75],[47,75],[47,73],[48,73],[48,71],[51,71],[51,69],[53,69],[53,67],[55,67],[55,65],[57,65],[57,63],[59,63],[59,60],[61,60],[61,59],[64,59],[64,57],[65,57],[65,55],[67,55],[67,53],[69,53],[69,51],[71,51],[71,49],[73,49],[73,47],[75,47],[75,46],[77,46],[77,42],[79,42],[79,40],[81,40],[81,39],[83,39],[83,37],[85,37],[85,34],[87,34],[87,35],[89,35],[89,31],[91,31],[91,30],[93,30],[93,26],[95,26],[95,24],[97,24],[97,22],[99,22],[99,20],[101,20],[101,21],[103,21],[103,15],[105,15],[105,14],[107,14],[107,10],[109,10],[109,6],[111,6],[111,9],[113,9],[113,7],[115,7],[115,4],[117,4],[117,0],[119,0],[119,2],[121,2],[121,5],[123,5],[123,3],[125,3],[125,8],[127,8],[127,1],[129,1],[129,11],[131,11],[131,12],[133,12],[133,16],[135,16],[135,13],[137,13],[137,17],[139,17],[139,18],[141,18],[141,19],[143,19],[143,23],[145,23],[145,25],[147,25],[147,27],[149,27],[149,28],[151,28],[151,29],[153,29],[153,32],[155,32],[155,33],[157,33],[157,36],[159,36],[159,38],[161,38],[161,41],[163,41],[163,43],[165,43],[165,44],[167,44],[167,45],[169,45],[169,48],[171,48],[171,50],[173,50],[173,52],[175,52],[175,54],[177,54],[177,56],[179,56],[179,58],[181,58],[181,61],[183,61],[183,62],[185,62],[185,64],[187,64],[187,66],[189,66],[189,68],[191,68],[191,70],[194,70],[194,72],[195,72],[195,74],[197,74],[197,76],[201,76],[201,78],[200,78],[200,80],[203,80],[203,82],[204,82],[204,84],[208,84],[208,86],[209,86],[209,88],[212,88],[212,90],[213,90],[213,92],[216,92],[216,94],[217,94],[217,96],[221,96],[221,98],[224,98],[224,100],[223,100],[223,102],[228,102],[228,104],[230,104],[230,106],[231,106],[231,108],[233,108],[233,110],[238,110],[238,112],[234,112],[234,114],[239,114],[239,116],[242,116],[242,118],[246,118],[246,120],[240,120],[240,122],[237,122],[237,124],]
;
const n = ar.length;
  createCanvas(250 * mul + mul, 250 * mul + mul);
  background(250)
  plot(ar,n);
}

function plot(ar, n) {
  stroke(220)
  for(let i = 0; i < n; i++) {
    let j = (i+1)%n;
    line(ar[i][0]*mul + mul , ar[i][1]*mul + mul , ar[j][0]*mul + mul , ar[j][1]*mul + mul )
  }
  stroke('red')
  for (let x of ar) {
    point(x[0]*mul + mul, x[1] * mul + mul)
  }
  stroke('blue')
  noFill();
  rectMode(CORNERS)
  rect(ar[248][0]*mul + mul, ar[248][1]*mul + mul, ar[218][0]*mul + mul, ar[218][1]*mul + mul)
}

*/

```
