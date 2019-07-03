# ICPC cheatsheet

## テンプレート
```cpp
#include<bits/stdc++.h>
#define rep(i,a,b) for(int i=int(a);i<int(b);++i)
using namespace std;
typedef long long ll;
int INF = (1LL << 30) - 1;
int MOD = 1e9+7;
main(){
    
}
```
以下に記述するソースコードは上記のテンプレートの使用を前提とする
## 入出力

### input
```cpp
int a;
cin >> a;
```
### output
```cpp
int a = 10;
cout << a;
```

### file input
`$ a.exe < input.txt`

### file output
`$ a.exe > output.txt`

### file input & output
`$ a.exe < input.txt > output.txt`

## コンパイルコマンド等
### compile
`$ g++ source.cpp`

### compile + optimize option
`$ g++ source.cpp -O3`

## STL
以下のSTLについて宣言方法や操作を記述する

+ std::string
+ std::vector
+ std::deque
+ std::set
+ std::map

コンテナクラス内に入れる型はintとしている（使用するときに書き換えること）
### std::string
文字列を扱う
#### 宣言・初期化
```cpp
string str; 
string str2(5, 'a'); // str2 == "aaaaa"
string str3 = "foo"; // str3 == "foo"
```
#### 入出力
```cpp
cin >> str >> endl;
cout << str << endl;
```
#### 追加
```cpp
str = "ab";
str += "cd"; // str == "abcd"
str += 'e'; // str == "abcde"
```
#### 削除
```cpp
str = "012345";
str.pop_back(); // str == "01234"
str.erase(str.begin() + 1, str.begin() + 3); // str == "034" 
```
#### サイズ取得
```cpp
str = "01234";
int N = str.size(); // N = 5
```
#### 部分文字列取得
str.substr(位置, サイズ)で部分文字列を取得する
```cpp
str = "01234";
sub = str.substr(1, 2); // sub == "12"
```
#### 検索
str.find(文字列)で文字列を検索できる
文字列が見つからなかった場合size_tの最大値（intの-1に相当）を返す
```cpp
str = "abcdef";
cout << (int)str.find("bcd") << endl; // 1
cout << (int)str.find("dbd") << endl; // -1
```
#### 数値→string
```cpp
string s = to_string(1234);
```
#### string→数値
```cpp
int num = stoi("1234");
```
### std::vector
可変長配列を扱う
#### 宣言・初期化
vectorは宣言時に引数を追加することでサイズや初期化する値を変えることができる
```cpp
vector<int> v; 
vector<int> v1(100); // 要素数100で初期化
vector<int> v2(10, 999); //要素数10 値999で初期化
```

#### 参照
vectorの要素参照は配列と同じようにできる
```cpp
v1[0] = 5;
cout << v1[0] << endl; // 5
```
iteratorを使っても同じようなことができる
```cpp
auto itr = v1.begin();
cout << *itr << endl; // 5
```
#### 追加
+ push_back(値)
+ insert(iterator, 値)
push_back()で末尾追加
insert()で任意部分に追加できる
insert()は挿入にO(N)時間かかるため注意 
```cpp
vector<int> vec;
vec.push_back(0); // {0}
vec.push_back(1); // {0,1}
vec.push_back(2); // {0,1,2};
vec.insert(vec.begin() + 1, 3); // {0,3,1,2}
```
#### 削除
+ pop_back()
+ erase(iterator, iterator)
pop_back()で末尾削除
erase()で任意部分の削除ができる
```cpp
vector<int> vec{0,1,2,3,4,5};
vec.pop_back(); // {0,1,2,3,4}
vec.erase(vec.begin() + 1, vec.begin() + 3); // {0,3,4}
```
#### サイズ取得
```cpp
vector<int> vec(5);
cout << vec.size() << endl; // 5
```
#### algorithmとの組み合わせ
algorithmと組み合わせることでよく行う操作が簡潔に書ける
よく使う関数を以下に記述する
##### ソート
sort()でクラスのsortが行える
標準では昇順ソートだが、逆イテレータや比較関数(greater)を渡すことによって降順にすることも可能である
```cpp
vector<int> vec{3,1,4,1,5,9,2};
sort(vec.begin(), vec.end()); //昇順ソート {1,1,2,3,4,5,9}
sort(vec.rbegin(), vec.rend()); //降順ソート {9,5,4,3,2,1,1}
sort(vec.begin(), vec.end(), [](int a, int b){
  return a > b;
});// ラムダ式で比較関数を渡す例 降順ソート
```
##### 反転
reverse()でvectorを反転させることができる
```cpp
vector<int> vec{1,2,3,4,5};
reverse(vec.begin(), vec.end()); // {5,4,3,2,1}
```
##### 二分探索
+ binary_search(iterator, iterator, value)
+ lower_bound(iterator, iterator, value)
+ upper_bound(iterator, iterator, value)
binary_search()はソートされているvector内で要素(value)を検索できる(見つかった場合true)
lower_bound()はvector内でvalue以上の値のうち最も左の要素
upper_bound()はvector内でvalueより大きい値のうち最も左の要素
```cpp
vector<int> vec{1,1,2,2,3,4};
cout << binary_search(vec.begin(), vec.end(), 3) << endl; // true
auto itr1 = lower_bound(vec.begin(), vec.end(), 2);
auto itr2 = upper_bound(vec.begin(), vec.end(), 2);
cout << (itr1 - vec.begin()) << endl; // 2
cout << (itr2 - vec.begin()) << endl; // 4
```
### std::deque
双方向キューを扱う
参照が高速
先頭・末尾の追加・削除が高速
#### 宣言・初期化
```cpp
deque<int> deq;
deque<int> deq1{1,2,3,4,5,6,7,8};
```
#### 参照
配列と同じように参照が行える
```cpp
deque<int> deq{1,2,3};
cout << deq[2] << endl; // 3
```
先頭と末尾はそれぞれfront(),back()という関数でできる
```cpp
deque<int> deq{1,2,3};
cout << deq.front() << endl; // 1
cout << deq.back() << endl; // 3
```
#### 追加
先頭・末尾追加はpush_front(), push_back()で行える
```cpp
deque<int> deq{1};
deq.push_front(0); // {0,1}
deq.push_back(2); // {0,1,2}
```
#### 削除
先頭・末尾削除はpop_front(), pop_back()で行える
```cpp
deque<int> deq{1,2,3};
deq.pop_front(); // {2,3}
deq.pop_back(); // {2}
```
#### サイズ取得
size()でサイズ取得ができる
```cpp
deque<int> deq{1,2,3,4};
cout << deq.size() << endl; // 4
```
### std::set
重複なしの集合を扱う
追加・削除・検索が高速である
内部では二分木構造であるためソートされている
#### 宣言・初期化
```cpp
set<int> st;
set<int> st1{3,1,4};
```
#### 参照
参照はイテレータを用いる
```cpp
set<int> st{3,1,4};
cout << st.begin() << endl; // 3
```
#### 追加
追加はinsert()を用いる
```cpp
set<int> st;
st.insert(5); // {5}
```
#### 削除
削除はerase()を用いる
```cpp
set<int> st{3,1,4};
st.erase(4); // {1,3}
```
#### サイズ取得
size()でサイズ取得ができる
```cpp
set<int> st{3,1,4};
cout << st.size() << endl; // 3
```
#### 検索
count()で要素の検索ができる
返り値は要素の個数
```cpp
set<int> st{3,1,4};
cout << st.count(3) << endl; // 1 
```
#### 二分探索
setでもlower_bound()等は使用できるが、vectorとは書き方が違う
```cpp
set<int> st{1,2,3,3,5};
auto itr = st.lower_bound(3);

```

### std::map
連想配列を扱う
#### 宣言・初期化
mapの宣言は<キー,値>で行う
```cpp
map<int,int> mp;
```
#### 参照
配列のように参照が行える
一度もアクセスしたことにないキーの場合新しく要素が作られるため注意
```cpp
map<int,int> mp;
mp[5] = 500;
cout << mp[5] << endl; // 500
cout << mp[10000000] << endl; // 0
```
#### 検索
find(key)でkeyが存在するか調べることができる
```cpp
map<int,int> mp;
mp[5] = 500;
auto itr = mp.find(5); // 存在する場合keyへのイテレータが帰ってくる
auto itr2 = mp.find(1); // 存在しない場合mp.end()が帰ってくる
```
#### 全要素の参照
mapは拡張for文で容易に全要素への参照が行える
```cpp
map<int,int> mp;
mp[0] = 1;
mp[1] = 2;
mp[2] = 3;
for(auto p:mp){
  // pの型はpair<key, value>
  // p.firstで昇順ソートされている
  cout << p.first << " " << p.second << endl;
}
```

## ライブラリ

### いろいろ
・二分探索
・累積和
・座圧
・しゃくとり法
・LIS
・編集距離
・next_perutation
### データ構造
・Union-Find
・BIT　セグ木
### 数理
・ユークリッドの互除法
・素数判定
・素因数分解
・約数列挙
・エラトステネスの篩
・mod関連
### グラフ

・DFS
・BFS
・ダイクストラ
・ワーシャルフロイド
・ベルマンフォード
・トポロジカルソート
・木の直径
・木の高さ
・LCA
