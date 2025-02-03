# codeforces-solutions
My recent Submission for Very (2000+ rated questions) Easy Explanation and Codes(c++)

p1 : https://codeforces.com/problemset/problem/2/B

Code : c++

#include <bits/stdc++.h>
using namespace std;

#define PB push_back
#define PF push_front
#define MP make_pair
#define FF first
#define SS second
#define _sz(x) (int)x.size()

typedef long long ll;
typedef long double ld;
typedef pair <int, int> pii;

int const N = 1000 + 20, inf = 1e9 + 20;
int n, t[N][N][2], d[N][N][2];
int zero = -1;

void spit (int x, int y, int k){
	if (x == 1 && y == 1) return;
	if (d[x - 1][y][k] < d[x][y - 1][k]) spit(x - 1, y, k), cout << 'D';
	else spit(x, y - 1, k), cout << 'R';
}

int main(){
	ios::sync_with_stdio(false); cin.tie(0); cout.tie(0);
	cin >> n;
	for (int i = 1; i <= n; i ++)
	  	for (int j = 1; j <= n; j ++){
		 	int a; cin >> a;
			if (!a) zero = i;
			while (a && a % 2 == 0) a /= 2, t[i][j][0] ++;
			while (a && a % 5 == 0) a /= 5, t[i][j][1] ++;
		}
	for (int i = 2; i <= n; i ++)
	  	for (int j = 0; j < 2; j ++)
		  	d[0][i][j] = d[i][0][j] = inf;
	for (int i = 1; i <= n; i ++)
	  	for (int j = 1; j <= n; j ++)
		  	for (int k = 0; k < 2; k ++)
			  	d[i][j][k] = min(d[i - 1][j][k], d[i][j - 1][k]) + t[i][j][k];
	int k = d[n][n][1] < d[n][n][0];
	if (~zero && d[n][n][k]){
	  	cout << "1\n";
		for (int i = 0; i < zero - 1; i ++) cout << 'D';
		for (int i = 0; i < n - 1; i ++) cout << 'R';
		for (int i = 0; i < n - zero; i ++) cout << 'D';
		cout << '\n';
	  	return 0;
	}
	cout << d[n][n][k] << '\n';
	spit(n, n, k); cout << '\n';
}

  
