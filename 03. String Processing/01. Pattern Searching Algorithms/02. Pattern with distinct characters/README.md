# Pattern searching (pattern consists of different characters)
The idea is to instead of sliding window by one character, we slide it by the length of previous window that matched. If previous window length that matched was zero, we slide the window by one character.

### sample input
```
4
ABCABCD
ABCD
ABCABCDABCD
ABCD
GEEKSFORGEEKS
EKS
ABCAAAD
ABD
```

### sample output
```
3
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

void naiveSearchDistinct(string txt, string pat)
{
	int m = txt.length();
	int n = pat.length();
	bool ok = 0;
	for (int i = 0; i <= m - n; ) {
		int j;
		for (j = 0; j < n; j++) {
			if (txt[i + j] != pat[j]) break;
		}
		if (j == n) {
			cout << i << " ";
			ok = 1;
		}
		if (j == 0) {
			i += 1;
		}
		else {
			i += j;
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
		naiveSearchDistinct(txt, pat);
	}


	return 0;
}
