# Rabin Karp Algorithm
In Rabin Karp Algorithm, we compare hash value of pattern with hash value of current window with a rolling hash function. </br></br>
**Time Complexity: O(|txt| + |pat|)**

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
#define nl	"\n"
#define ll	long long
#define pb	push_back
#define mp	make_pair
#define pii	pair<int, int>
#define rep(i, n)	for (int i = 0; i < (int) n; i++)
#define repr(i, a, b)	for (int i = (int) a; i <= (int) b; i++)

void fio()
{
	ios_base::sync_with_stdio(0);
	cin.tie(0);
	cout.tie(0);
}

void RabinKarp(string txt, string pat)
{
	int m = txt.length();
	int n = pat.length();
	ll p = 31;
	ll mod = 1e9 + 9;
	ll power[m + 1];
	power[0] = 1;
	for (int i = 1; i < m + 1; i++) {
		power[i] = (power[i - 1] * p) % mod;
	}
	ll hash_pat = 0;
	for (int i = 0; i < n; i++) {
		hash_pat = (hash_pat + mod + ((pat[i] - 'a' + 1) * (power[i])) % mod) % mod;
	}
	vector<ll> hash_txt(m + 1, 0);
	for (int i = 0; i < m; i++) {
		hash_txt[i + 1] = (hash_txt[i] + mod + ((txt[i] - 'a' + 1) * (power[i])) % mod) % mod;
	}
	vector<int> occurences;
	for (int i = 0; i <= m - n; i++) {
		ll curr_window_hash = (hash_txt[i + n] - hash_txt[i] + mod) % mod;
		if (curr_window_hash == (hash_pat * power[i]) % mod) {
			occurences.pb(i);
		}
	}
	if (occurences.size() == 0) {
		cout << "NOT FOUND" << nl;
	}
	else {
		for (int x : occurences) {
			cout << x << " ";
		}
		cout << nl;
	}
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
		RabinKarp(txt, pat);
	}


	return 0;
}
```
