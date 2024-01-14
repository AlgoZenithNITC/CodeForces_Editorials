𝗣𝗿𝗼𝗯𝗹𝗲𝗺𝘀 𝗔 :  Satisfying Constraints

𝗧𝗼𝗽𝗶𝗰𝘀: Greedy,Schedules.

 Hint 1 :- Think of computing upper_bound & lower_bound for all the set of numbers satisfy the given constraints. (This can be computed just using the Type -1 & Type-2 constraints)

Hint 2 :- After figuring out the range of numbers that satisfy the given constraints ,How is about excluding those numbers of Type-3 constraints that fall under this range that we previously computed.

Code : (in c++)

 #include<bits/stdc++.h>
using namespace std;
int main()
{
    int t;
    cin>>t;
    for(int i=0;i<t;i++)
    {
        int n;
        cin>>n;
        vector<int>temp;
        int upperlimit=1e9;
        int lowerlimit=1;
        for(int i=0;i<n;i++)
        {
            int num,x;
            cin>>num>>x;
            if(num==1)
            lowerlimit=max(lowerlimit,x);
            else if(num==2)
            upperlimit=min(upperlimit,x);
            else
            temp.push_back(x);
        }
        if(upperlimit<lowerlimit)
        {
            cout<<0<<endl;
        }
        else
        {
            int ans=upperlimit-lowerlimit+1;
            for(int i=0;i<(int)temp.size();i++)
            {
                if(lowerlimit<=temp[i] && temp[i]<=upperlimit)
                ans--;
            }
            cout<<ans<<endl;
        }
    }
    return 0;
}

Code: (in Java)
import java.util.Scanner;
import java.util.Vector;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int t = scanner.nextInt();

        for (int testCase = 0; testCase < t; testCase++) {
            int n = scanner.nextInt();
            Vector<Integer> temp = new Vector<>();
            int upperLimit = 1_000_000_000;
            int lowerLimit = 1;

            for (int i = 0; i < n; i++) {
                int num = scanner.nextInt();
                int x = scanner.nextInt();

                if (num == 1) {
                    lowerLimit = Math.max(lowerLimit, x);
                } else if (num == 2) {
                    upperLimit = Math.min(upperLimit, x);
                } else {
                    temp.add(x);
                }
            }

            if (upperLimit < lowerLimit) {
                System.out.println(0);
            } else {
                int ans = upperLimit - lowerLimit + 1;

                for (int i = 0; i < temp.size(); i++) {
                    if (lowerLimit <= temp.get(i) && temp.get(i) <= upperLimit) {
                        ans--;
                    }
                }

                System.out.println(ans);
            }
        }
    }
}

Code: (in Python)
t = int(input())

for _ in range(t):
    n = int(input())
    temp = []
    upper_limit = 10**9
    lower_limit = 1

    for _ in range(n):
        num, x = map(int, input().split())
        if num == 1:
            lower_limit = max(lower_limit, x)
        elif num == 2:
            upper_limit = min(upper_limit, x)
        else:
            temp.append(x)

    if upper_limit < lower_limit:
        print(0)
    else:
        ans = upper_limit - lower_limit + 1
        for i in temp:
            if lower_limit <= i <= upper_limit:
                ans -= 1
        print(ans)


Time complexity  : - O(n) , since we are traversing whole n constraints at most twice.

𝗣𝗿𝗼𝗯𝗹𝗲𝗺 B : Summation Game

𝗧𝗼𝗽𝗶𝗰𝘀 :- sorting,Prefixsum,Greedy,simulation

Hint 1 : - After ALice operations was done , what could bob do to minimize the summation.

Explanation :- 
Since, After ALice operation was performed,Bob will pick atmost x maximum elements form the remaining array so that the summation would be as minimum as possible.

Now , But what could be the optimal way to perform Alice operation.since Alice can remove atmost K elements form the array.The optimal way to achieve the maximum sumation is by removing (atmost K) maximum elements from the array.

But why, so let's assume ALice did not remove any element ,Then the summation of atmost x(elements selected by Bob) maximum elements be X.And summation of remaining elements be Y.
If alice want to remove one element lets it be number 'a' from the x elements which were previously selected by Bob. Since, one element is reduced from the set of elemets selected by Bob,Now Bob has to pick one more element.Bob always picks the maximum element form the remaining element to compensate the count of 'x', lets it be 'b'; 

The optimal sum before ALice removing one element is Y - X .
The optimal sum after ALice removing one element (i.e is 'a' )
(Y-b) - (X-a+b). This expression gives (X-Y + (a-2*b) ).
Here, additional term added is (a-2*b).This would the maximum possible value if 'a' is as maximum as possible.Hence, ALice always removes the maximum elements from the array.

Therfore , iterate over all 'i' (from o to K) values that can be possibly removed by ALice and thus the removed 'i' elements must be 'i' maximum elements from the whole array.
 
 

Code : (in c++) 

#include<bits/stdc++.h>
using namespace std;

int main()
{
    int t;
    cin>>t;
    for(int i=0;i<t;i++)
    {
        int n,k,x;
        cin>>n>>k>>x;
        int a[n];
        for(int i=0;i<n;i++)
        {
            cin>>a[i];
        }
        sort(a,a+n);
        int prev[n+1];
        prev[0]=0;
        for(int i=0;i<n;i++)
        {
            prev[i+1]=prev[i]+a[i];
        }
        
        int t=min(k,n);
        int ans=INT_MIN;
        for(int i=0;i<=t;i++)
        {
            if(x>=(n-i))
            ans=max(ans,-1*prev[n-i]);
            else
            ans=max(ans,-1*prev[n-i] + 2*prev[n-i-x] );
        }
        cout<<ans<<endl;
    }
    return 0;
}

Code : (in Java) 

import java.util.Arrays;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int t = scanner.nextInt();

        for (int testCase = 0; testCase < t; testCase++) {
            int n = scanner.nextInt();
            int k = scanner.nextInt();
            int x = scanner.nextInt();

            int[] a = new int[n];
            for (int i = 0; i < n; i++) {
                a[i] = scanner.nextInt();
            }

            Arrays.sort(a);

            int[] prev = new int[n + 1];
            prev[0] = 0;
            for (int i = 0; i < n; i++) {
                prev[i + 1] = prev[i] + a[i];
            }

            int tValue = Math.min(k, n);
            int ans = Integer.MIN_VALUE;

            for (int i = 0; i <= tValue; i++) {
                if (x >= (n - i))
                    ans = Math.max(ans, -1 * prev[n - i]);
                else
                    ans = Math.max(ans, -1 * prev[n - i] + 2 * prev[n - i - x]);
            }

            System.out.println(ans);
        }
    }
}

Code: (in Python)
t = int(input())

for _ in range(t):
    n, k, x = map(int, input().split())
    a = list(map(int, input().split()))

    a.sort()
    prev = [0] * (n + 1)

    for i in range(n):
        prev[i + 1] = prev[i] + a[i]

    t = min(k, n)
    ans = float('-inf')

    for i in range(t + 1):
        if x >= (n - i):
            ans = max(ans, -1 * prev[n - i])
        else:
            ans = max(ans, -1 * prev[n - i] + 2 * prev[n - i - x])

    print(ans)



Time complexity :- O( min(n,k) )

