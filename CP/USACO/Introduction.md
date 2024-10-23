# Input/Output
## Method 1:
```c++
#include <cstdio>

#include <iostream>

using namespace std;

// the argument is the input filename without the extension
void setIO(string s) {
	freopen((s + ".in").c_str(), "r", stdin);
	freopen((s + ".out").c_str(), "w", stdout);
}
int main() {
	setIO("problemname");
	int a,b,c;
	cin >> a >> b >> c;
	cout << "The sum of these three numbers is " << a + b + c << "\n";
}
```
## Method 2
```c++
#include <fstream>

using namespace std;

int main() {
	ifstream fin("problemname.in");
	ofstream fout("problemname.out");
	int a,b,c;
	fin >> a >> b >> c;
	fout << "The sum of these three numbers is " << a + b + c << "\n";
}
```
