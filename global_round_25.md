## Dual Trigger

<details>
<summary>Python</summary>

```python
def helper(n, s):
    if n == 1 and s == "0":
        return "YES"
    elif n == 2 and s == "00":
        return "YES"
    else:
        c = s.count('1')
        if c % 2 == 0:
            if c == 2:
                for i in range(len(s) - 1):
                    if s[i] == '1' and s[i + 1] == '1':
                        return "NO"
                return "YES"
            else:
                return "YES"
        return "NO"

def main():
    t = int(input())
    for _ in range(t):
        n, s = map(str, input().split())
        print(helper(int(n), s))

if __name__ == "__main__":
    main()
```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

string helper()
{
    int n ;
        string s;
        cin>>n>>s;
        if(n==1 && s=="0")
        return "YES\n";
        else if(n==2 && s == "00")
        return "YES\n";
        else 
        {
            int c = 0;
            for(char i : s)
            {
                if(i=='1')
                c++;
            }
            if(c%2==0)
            {
                if(c==2)
                {
                    for(int i = 0 ; i < s.size()-1 ; i++)
                    {
                        if(s[i]=='1' && s[i+1]=='1')
                        return "NO\n";
                    }
                    return "YES\n";
                }
                else
                {
                    return "YES\n";
                }
            }
            return "NO\n";
        }
        return "NO\n";
}

int main() {
    int t;
    cin>>t;
    while(t--)
    {
        cout<<helper();
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
        int t = scanner.nextInt();
        while (t-- > 0) {
            System.out.print(helper(scanner.nextInt(), scanner.next()) + "\n");
        }
    }

    public static String helper(int n, String s) {
        if (n == 1 && s.equals("0"))
            return "YES";
        else if (n == 2 && s.equals("00"))
            return "YES";
        else {
            int c = 0;
            for (char i : s.toCharArray()) {
                if (i == '1')
                    c++;
            }
            if (c % 2 == 0) {
                if (c == 2) {
                    for (int i = 0; i < s.length() - 1; i++) {
                        if (s.charAt(i) == '1' && s.charAt(i + 1) == '1')
                            return "NO";
                    }
                    return "YES";
                } else {
                    return "YES";
                }
            }
            return "NO";
        }
    }
}
```

</details>

## Battle Cows

<details>
<summary>Python</summary>

```python
def get_ans(a, n, p):
    maxa = 0
    ans = 0
    for i in range(1, n):
        if a[maxa] > a[i]:
            if p == maxa:
                ans += 1
            continue
        else:
            maxa = i
            if p == maxa:
                ans += 1
    return ans

def main():
    t = int(input())
    for _ in range(t):
        n, k = map(int, input().split())
        k -= 1

        a = list(map(int, input().split()))

        ans = get_ans(a, n, k)
        a[0], a[k] = a[k], a[0]
        ans = max(ans, get_ans(a, n, 0))
        a[0], a[k] = a[k], a[0]

        for i in range(n):
            if a[i] > a[k]:
                a[k], a[i] = a[i], a[k]
                ans = max(ans, get_ans(a, n, i))
                break

        print(ans)

if __name__ == "__main__":
    main()

```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

int getans(int a[],int n,int p)
{
    int maxa=0;
    int ans=0;
    for(int i=1;i<n;i++)
    {
        if(a[maxa]>a[i])
        {
            if(p==maxa){ans++;}
            continue;
        }
        else
        {
            maxa=i;
            if(p==maxa){ans++;}
        }
    }
    return ans;
}


int main()
{
   int t;
   cin>>t;

   while(t--)
   {
        int n,k;
        cin>>n>>k;
        k--;

        int a[n];
        for(int i=0;i<n;i++){cin>>a[i];}

        int ans=getans(a,n,k);
        swap(a[k],a[0]);
        ans=max(ans,getans(a,n,0));
        swap(a[k],a[0]);

        for(int i=0;i<n;i++)
        {
            if(a[i]>a[k])
            {
                swap(a[k],a[i]);
                ans=max(ans,getans(a,n,i));
                break;
            }
        }

        cout<<ans<<"\n";
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
        int t = scanner.nextInt();
        while (t-- > 0) {
            int n = scanner.nextInt();
            int k = scanner.nextInt() - 1;

            int[] a = new int[n];
            for (int i = 0; i < n; i++) {
                a[i] = scanner.nextInt();
            }

            int ans = getAns(a, n, k);
            int temp = a[k];
            a[k] = a[0];
            a[0] = temp;
            ans = Math.max(ans, getAns(a, n, 0));
            temp = a[k];
            a[k] = a[0];
            a[0] = temp;

            for (int i = 0; i < n; i++) {
                if (a[i] > a[k]) {
                    temp = a[i];
                    a[i] = a[k];
                    a[k] = temp;
                    ans = Math.max(ans, getAns(a, n, i));
                    break;
                }
            }

            System.out.println(ans);
        }
    }

    public static int getAns(int[] a, int n, int p) {
        int maxa = 0;
        int ans = 0;
        for (int i = 1; i < n; i++) {
            if (a[maxa] > a[i]) {
                if (p == maxa) {
                    ans++;
                }
                continue;
            } else {
                maxa = i;
                if (p == maxa) {
                    ans++;
                }
            }
        }
        return ans;
    }
}
```

</details>

## Ticket Hoarding

<details>
<summary>Python</summary>

```python
t = int(input())
for _ in range(t):
    n, m, k = map(int, input().split())
    a = list(map(int, input().split()))
    a.sort()
    ans = 0
    tax = 0
    for price in a:
        buy = min(m, k)
        ans += buy * (price + tax)
        tax += buy
        k -= buy
    print(ans)
```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t; cin >> t;
    while (t--) {
        int n, m, k; cin >> n >> m >> k;
        vector<int> a(n);
        for (int i = 0; i < n; i++) {
            cin >> a[i];
        }
        sort(a.begin(), a.end());
        int64_t ans = 0;
        int tax = 0;
        for (int i = 0; i < n; ++i) {
            int buy = min(m, k);
            ans += 1LL * buy * (a[i] + tax);
            tax += buy;
            k -= buy;
        }
        cout << ans << '\n';
    }
}
```

</details>

<details>
<summary>Java</summary>

```java
import java.util.Arrays;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int t = scanner.nextInt();
        while (t-- > 0) {
            int n = scanner.nextInt();
            int m = scanner.nextInt();
            int k = scanner.nextInt();

            int[] a = new int[n];
            for (int i = 0; i < n; i++) {
                a[i] = scanner.nextInt();
            }
            Arrays.sort(a);

            long ans = 0;
            int tax = 0;
            for (int i = 0; i < n; ++i) {
                int buy = Math.min(m, k);
                ans += (long) buy * (a[i] + tax);
                tax += buy;
                k -= buy;
            }
            System.out.println(ans);
        }
    }
}
```

</details>

## Buying Jewels

<details>
<summary>Python</summary>

```python
t = int(input())
for _ in range(t):
    n, k = map(int, input().split())
    if n < k:
        print("NO")
    elif n == k:
        print("YES\n1\n1")
    elif n < 2 * k - 1:
        print("NO")
    else:
        print("YES\n2\n{} 1".format(n - k + 1))
```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int t; cin >> t;
    while (t--) {
        int64_t n, k; cin >> n >> k;
        if (n < k) {
            cout << "NO\n";
        } else if (n == k) {
            cout << "YES\n1\n1\n";
        } else if (n < 2 * k - 1) {
            cout << "NO\n";
        } else {
            cout << "YES\n2\n" << n - k + 1 << " 1\n";
        }
    }
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
        int t = scanner.nextInt();
        while (t-- > 0) {
            long n = scanner.nextLong();
            long k = scanner.nextLong();
            if (n < k) {
                System.out.println("NO");
            } else if (n == k) {
                System.out.println("YES\n1\n1");
            } else if (n < 2 * k - 1) {
                System.out.println("NO");
            } else {
                System.out.println("YES\n2\n" + (n - k + 1) + " 1");
            }
        }
    }
}
```

</details>
