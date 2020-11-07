# Naive Pattern Searching Algorithm
The idea is to slide the window of pattern length over all possible windows of text and verify whether it matches or not for each window.
</br></br>
**Time Complexity: O((|txt|-|pat|+1)(|pat|))**

### sample input
```
6
ABABABCD
ABAB
ABCABCD
ABCD
AAAAA
AAA
ABCABCDABCD
ABCD
GEEKSFORGEEKS
EKS
ABCAAAD
ABD
```

### sample output
```
0 2
3
0 1 2
3 7
2 10
NOT FOUND
```

### code
```cpp
#include <bits/stdc++.h>
using namespace std;

void fio()
{
	ios_base::sync_with_stdio(0);
	cin.tie(0);
	cout.tie(0);
}

/* naive pattern search */
void naiveSearch(string txt, string pat)
{
	int m = txt.length();
	int n = pat.length();
	bool ok = 0;
	for (int i = 0; i <= m - n; i++) {
		int j;
		for (j = 0; j < n; j++) {
			if (txt[i + j] != pat[j]) break;
		}
		if (j == n) {
			cout << i << " ";
			ok = 1;
		}
	}
	if (!ok) {
		cout << "NOT FOUND";
	}
	cout << endl;
}


int main()
{
	fio();

#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif

	int t;
	string txt, pat;
	cin >> t;
	while (t--) {
		cin >> txt >> pat;
		naiveSearch(txt, pat);
	}


	return 0;
}
```
