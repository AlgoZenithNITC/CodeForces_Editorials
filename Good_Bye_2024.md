## A. Tender Carpenter

<details>
<summary>Python</summary>

```python
MAXN = 1001
a = [0] * MAXN

def solve():
    n = int(input())
    a[1:n+1] = map(int, input().split())
    for i in range(1, n):
        if 2 * min(a[i], a[i + 1]) > max(a[i], a[i + 1]):
            print("YES")
            return
    print("NO")

if __name__ == "__main__":
    t = int(input())
    for _ in range(t):
        solve()


```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <bits/stdc++.h>
 
#define MAXN 1001
int a[MAXN];
void solve() {
	int n; std::cin >> n;
	for (int i = 1; i <= n; ++i) std::cin >> a[i];
	for (int i = 1; i < n; ++i) if (2 * std::min(a[i], a[i + 1]) > std::max(a[i], a[i + 1])) 
		{ std::cout << "YES\n"; return; }
	std::cout << "NO\n";
}
 
int main() {
	std::ios::sync_with_stdio(false);
	std::cin.tie(nullptr), std::cout.tie(nullptr);
	int t; std::cin >> t; while (t--) solve(); return 0;
}
```

</details>

<details>
<summary>Java</summary>

```java
import java.util.*;

public class Main {
    static final int MAXN = 1001;
    static int[] a = new int[MAXN];

    static void solve(Scanner sc) {
        int n = sc.nextInt();
        for (int i = 1; i <= n; ++i) a[i] = sc.nextInt();

        for (int i = 1; i < n; ++i) {
            if (2 * Math.min(a[i], a[i + 1]) > Math.max(a[i], a[i + 1])) {
                System.out.println("YES");
                return;
            }
        }
        System.out.println("NO");
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();
        while (t-- > 0) solve(sc);
    }
}

```

</details>

## B. Outstanding Impressionist
<details>
<summary>Python</summary>

```python
import sys

MAXN = 400001
l = [0] * MAXN
r = [0] * MAXN
sum = [0] * MAXN
cnt = [0] * MAXN

def solve():
    n = int(sys.stdin.readline().strip())
    for i in range(1, 2 * n + 1):
        sum[i] = cnt[i] = 0
    for i in range(1, n + 1):
        l[i], r[i] = map(int, sys.stdin.readline().strip().split())
        if l[i] == r[i]:
            sum[l[i]] = 1
            cnt[l[i]] += 1
    for i in range(2, 2 * n + 1):
        sum[i] += sum[i - 1]
    result = []
    for i in range(1, n + 1):
        if l[i] == r[i]:
            result.append("1" if cnt[l[i]] <= 1 else "0")
        else:
            result.append("1" if sum[r[i]] - sum[l[i] - 1] < r[i] - l[i] + 1 else "0")
    print(''.join(result))

def main():
    input = sys.stdin.read
    data = input().splitlines()
    t = int(data[0])
    for _ in range(t):
        solve()

if _name_ == "_main_":
    main()
```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <bits/stdc++.h>
 
#define MAXN 400001
int l[MAXN], r[MAXN], sum[MAXN], cnt[MAXN];
void solve() {
	int n; std::cin >> n;
	for (int i = 1; i <= 2 * n; ++i) sum[i] = cnt[i] = 0;
	for (int i = 1; i <= n; ++i) {
		std::cin >> l[i] >> r[i];
		if (l[i] == r[i]) sum[l[i]] = 1, ++cnt[l[i]];
	}
	for (int i = 2; i <= 2 * n; ++i) sum[i] += sum[i - 1];
	for (int i = 1; i <= n; ++i) 
		std::cout << ((l[i] == r[i] ? cnt[l[i]] <= 1 : sum[r[i]] - sum[l[i] - 1] < r[i] - l[i] + 1) ? "1" : "0");
	std::cout << '\n';
}
int main() {
	std::ios::sync_with_stdio(false);
	std::cin.tie(nullptr), std::cout.tie(nullptr);
	int t; std::cin >> t; while (t--) solve(); return 0;
}
```

</details>

<details>
<summary>Java</summary>

```java
import java.util.Scanner;

public class Main {
    static final int MAXN = 400001;
    static int[] l = new int[MAXN];
    static int[] r = new int[MAXN];
    static int[] sum = new int[MAXN];
    static int[] cnt = new int[MAXN];

    public static void solve(Scanner scanner) {
        int n = scanner.nextInt();
        for (int i = 1; i <= 2 * n; ++i) {
            sum[i] = 0;
            cnt[i] = 0;
        }
        for (int i = 1; i <= n; ++i) {
            l[i] = scanner.nextInt();
            r[i] = scanner.nextInt();
            if (l[i] == r[i]) {
                sum[l[i]] = 1;
                ++cnt[l[i]];
            }
        }
        for (int i = 2; i <= 2 * n; ++i) {
            sum[i] += sum[i - 1];
        }
        StringBuilder result = new StringBuilder();
        for (int i = 1; i <= n; ++i) {
            result.append((l[i] == r[i] ? cnt[l[i]] <= 1 : sum[r[i]] - sum[l[i] - 1] < r[i] - l[i] + 1) ? "1" : "0");
        }
        System.out.println(result);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int t = scanner.nextInt();
        while (t-- > 0) {
            solve(scanner);
        }
        scanner.close();
    }
}
```

</details>

## C. Bewitching Stargazer

<details>
<summary>Python</summary>

```python
import sys

T = int(sys.stdin.readline().strip())

for _ in range(T):
    n, k = map(int, sys.stdin.readline().strip().split())
    mul = n + 1
    sum_ = 0
    cur = 1
    while n >= k:
        if n & 1:
            sum_ += cur
        n >>= 1
        cur <<= 1
    print(mul * sum_ // 2)
```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <bits/stdc++.h>
#define int long long
 
using namespace std;
 
int T;
int n, k;
 
signed main() {
	cin >> T;
	while (T--) {
		cin >> n >> k;
		int mul = n + 1, sum = 0, cur = 1;
		while (n >= k) {
			if (n & 1) sum += cur;
			n >>= 1;
			cur <<= 1;
		}
		cout << mul * sum / 2 << endl;
	}
	return 0;
}
```

</details>

<details>
<summary>Java</summary>

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        long T = scanner.nextLong();
        while (T-- > 0) {
            long n = scanner.nextLong();
            long k = scanner.nextLong();
            long mul = n + 1, sum = 0, cur = 1;
            while (n >= k) {
                if ((n & 1) == 1) sum += cur;
                n >>= 1;
                cur <<= 1;
            }
            System.out.println(mul * sum / 2);
        }
        scanner.close();
    }
}

```

</details>

## D. Refund Product Optimality

<details>
<summary>Python</summary>

```python
MOD = 998244353

def qpow(a, x = MOD - 2):
    res = 1
    while x > 0:
        if x & 1:
            res = res * a % MOD
        a = a * a % MOD
        x >>= 1
    return res

def solve():
    n, q = map(int, input().split())
    a = [0] + list(map(int, input().split()))
    b = [0] + list(map(int, input().split()))
    c = sorted(a[1:])
    d = sorted(b[1:])

    res = 1
    for i in range(n):
        res = res * min(c[i], d[i]) % MOD

    print(res, end=" ")
    for _ in range(q):
        op, x = map(int, input().split())
        if op == 1:
            p = next(i for i in range(len(c)) if c[i] > a[x]) - 1
            if c[p] < d[p]:
                res = res * qpow(c[p]) % MOD * (c[p] + 1) % MOD
            a[x] += 1
            c[p] += 1
        else:
            p = next(i for i in range(len(d)) if d[i] > b[x]) - 1
            if d[p] < c[p]:
                res = res * qpow(d[p]) % MOD * (d[p] + 1) % MOD
            b[x] += 1
            d[p] += 1
        print(res, end=" " if _ < q - 1 else "\n")

if __name__ == "__main__":
    t = int(input())
    for _ in range(t):
        solve()

```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

constexpr int MOD = 998244353;

int qpow(int a, int x = MOD - 2) {
    int res = 1;
    while (x) {
        if (x & 1) res = 1LL * res * a % MOD;
        a = 1LL * a * a % MOD;
        x >>= 1;
    }
    return res;
}

void solve() {
    int n, q;
    cin >> n >> q;

    vector<int> a(n + 1), b(n + 1), c(n + 1), d(n + 1);
    for (int i = 1; i <= n; ++i) cin >> a[i], c[i] = a[i];
    for (int i = 1; i <= n; ++i) cin >> b[i], d[i] = b[i];

    sort(c.begin() + 1, c.end());
    sort(d.begin() + 1, d.end());

    int res = 1;
    for (int i = 1; i <= n; ++i)
        res = 1LL * res * min(c[i], d[i]) % MOD;

    cout << res << " \n"[q == 0];

    while (q--) {
        int op, x;
        cin >> op >> x;

        if (op == 1) {
            int p = upper_bound(c.begin() + 1, c.end(), a[x]) - c.begin() - 1;
            if (c[p] < d[p]) 
                res = 1LL * res * qpow(c[p]) % MOD * (c[p] + 1) % MOD;
            ++a[x];
            ++c[p];
        } else {
            int p = upper_bound(d.begin() + 1, d.end(), b[x]) - d.begin() - 1;
            if (d[p] < c[p]) 
                res = 1LL * res * qpow(d[p]) % MOD * (d[p] + 1) % MOD;
            ++b[x];
            ++d[p];
        }
        cout << res << " \n"[q == 0];
    }
}

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int t;
    cin >> t;
    while (t--) solve();

    return 0;
}

```

</details>

<details>
<summary>Java</summary>

```java
import java.util.*;

public class Main {
    static final int MOD = 998244353;

    static int qpow(int a, int x) {
        int res = 1;
        while (x > 0) {
            if ((x & 1) == 1) res = (int)((1L * res * a) % MOD);
            a = (int)((1L * a * a) % MOD);
            x >>= 1;
        }
        return res;
    }

    static void solve(Scanner sc) {
        int n = sc.nextInt();
        int q = sc.nextInt();

        int[] a = new int[n + 1];
        int[] b = new int[n + 1];
        int[] c = new int[n + 1];
        int[] d = new int[n + 1];

        for (int i = 1; i <= n; ++i) {
            a[i] = sc.nextInt();
            c[i] = a[i];
        }
        for (int i = 1; i <= n; ++i) {
            b[i] = sc.nextInt();
            d[i] = b[i];
        }

        Arrays.sort(c, 1, n + 1);
        Arrays.sort(d, 1, n + 1);

        int res = 1;
        for (int i = 1; i <= n; ++i) {
            res = (int)((1L * res * Math.min(c[i], d[i])) % MOD);
        }

        System.out.print(res + " ");
        for (int i = 1; i <= q; ++i) {
            int op = sc.nextInt();
            int x = sc.nextInt();

            if (op == 1) {
                int p = Arrays.binarySearch(c, 1, n + 1, a[x]);
                if (p < 0) p = -p - 2;
                if (c[p] < d[p]) res = (int)((1L * res * qpow(c[p], MOD - 2) % MOD) * (c[p] + 1) % MOD);
                a[x]++;
                c[p]++;
            } else {
                int p = Arrays.binarySearch(d, 1, n + 1, b[x]);
                if (p < 0) p = -p - 2;
                if (d[p] < c[p]) res = (int)((1L * res * qpow(d[p], MOD - 2) % MOD) * (d[p] + 1) % MOD);
                b[x]++;
                d[p]++;
            }
            System.out.print(res + (i == q ? "\n" : " "));
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();
        while (t-- > 0) solve(sc);
    }
}

```

</details>
