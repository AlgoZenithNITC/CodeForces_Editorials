## A. MEX TABLE

<details>
<summary>Python</summary>

```python
t = int(input())
for _ in range(t):
    print(max(map(int, input().split()))+1)

```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    int t;
    cin>>t;
    while(t--){
        int n, m;
        cin>>n>>m;
        cout<<max(m, n)+1<<'\n';
    }
    return 0;
}
```

</details>

<details>
<summary>Java</summary>

```java

import java.util.*;
public class Mex
{
	public static void main(String[] args) {
		Scanner sc=new Scanner(System.in);
		int T=sc.nextInt();
		while(T-->0){
		    int m=sc.nextInt();
		    int n=sc.nextInt();
		    int ans=Math.max(m,n);
		    System.out.println((ans+1));
		}
	}
}

```

</details>

## B. Gorilla and The Exam
<details>
<summary>Python</summary>

```python
from collections import Counter
 
for _ in range(int(input())):
	a, c = map(int,input().split())
	l = Counter(input().split())
	m = len(l)
	for i in sorted(l.values()):
		if c<i:
			break
		c-=i
		m-=1
	print(max(1,m))
```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include<bits/stdc++.h>
using namespace std;

int main(){
    int t;
    cin>>t;
    while(t--){
        int n, k;
        cin>>n>>k;
        vector<int> a(n);
        for(int i = 0; i < n; i++) { 
            cin>>a[i];
        }
        sort(a.begin(), a.end());
        vector<int> freq = {1};
        for(int i = 1; i < n; i++){
            if(a[i] == a[i - 1])
                freq.back()++;
            else
                freq.push_back(1);
        }
        sort(freq.begin(), freq.end());
        int d = freq.size();
        int ans = 1;
        for(int i = 0; i < d; i++){
            if(k >= freq[i])
                k -= freq[i];
            else{
                ans = d - i;
                break;
            }
        }
        cout<<ans<<'\n';
    }
    return 0;
}
```

</details>

<details>
<summary>Java</summary>

```java
import java.util.*;
import java.lang.*;
import java.io.*;

public class Codeforces{
	
	public static int solve(int n, int[] arr, int k){
		HashMap<Integer,Integer> map = new HashMap<>();
		for(int i : arr){
			map.put(i,map.getOrDefault(i,0)+1);
		}
		ArrayList<Integer> list = new ArrayList<>();
		for(int i : map.keySet()){
			list.add(map.get(i));
		}
		Collections.sort(list);
		int count = 0;
		for(int i : list){
			if(i<=k){
				k -= i;
			}else{
				count ++;
			}
		}
		return Math.max(1,count);
    }
		
	public static void main(String[] args){
		Scanner sc = new Scanner(System.in);
		int test = sc.nextInt();
		while(test-->0){
			int n = sc.nextInt();
			int k = sc.nextInt();
			int[] arr = new int[n];
			for(int i = 0; i<n; i++){
					arr[i]=sc.nextInt();
			}
			System.out.println(solve(n,arr,k));
		}
	}
}
```

</details>

## C. Trip To The Olympiad

<details>
<summary>Python</summary>

```python
import math

for _ in range(int(input())):
    l, r = [int(x) for x in input().split()]
    c = l&r
    a = ~c
    ra = a & r

    x = math.floor(math.log(ra, 2))

    a = 2**int(x)
    b = a-1

    # print("pre",a,b,c)

    add = ~(a|b) & r
    a += add
    b += add

    c = a+1 if a != r else b-1

    print(a,b,c)
```

</details>

<details>
<summary>Cpp</summary>

```cpp
#include<bits/stdc++.h>
using namespace std;

int bitNumber(int num){
    int n = (floor(log2(num)) + 1);
    int ans = 1;
    for(int i = n; i >= 0; i--){
        if((num >> i) & 1){
            ans = i;
            break;
        }
    }
    return ans;
}

void solve(int l, int r){
    int k = bitNumber(l ^ r);
    int x = l | ((1<<k) - 1);
    int y = x + 1;
    int z = (x == l) ? r : l;
    cout<<x<<' '<<y<<' '<<z<<'\n';
}

int main(){
    int t;
    cin>>t;
    while(t--){
        int l, r;
        cin>>l>>r;
        solve(l, r);
    }
    return 0;
}

```

</details>

<details>
<summary>Java</summary>

```java
import java.util.Scanner;

public class OlympiadTrip {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int t = sc.nextInt();

        while(t-->0){
            int l = sc.nextInt();
            int r = sc.nextInt();

            int k = 31 - Integer.numberOfLeadingZeros(l^r);
            int a = l | ((1 << k) -1);
            int b = a + 1;
            int c = (a == l? r : l); 
            
            System.out.println(a + " " + b + " " + c);
        }

        sc.close();
    }
}

```

</details>
