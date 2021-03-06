# cc-total-mined
## 結論
使用は自己責任で    
[ここ](https://nao20010128nao.github.io/cc-total-mined/)からどうぞ

## これって何
仮想通貨の総採掘量を**簡単に**計算します     
実際のネットワークやブロックチェーンとは無関係に計算するので本当の総採掘量とは異なることがあります

## どうやって計算するの
Insightを開いて目に止まった[この](https://insight.bitpay.com/block/0000000000000000005d7c5db804b5c63aff09c3399b178915e4217f3b95249a)ブロックを例に解説します
    
Bitcoinフォークの仮想通貨には、*半減期*というものが存在します    
*半減期*とは一定のブロックごとに報酬を半減させるというものです    
例えば、Bitcoinでは、最初は50BTCであった報酬が、210000ブロックごとに半減していき、2018/02/11時点では12.5BTCとなっています    
半減期とは、この210000ブロックを指します    
この半減期ごとに一々計算してはラチがあかないので、0ブロック目から最後の半減期まで一括で計算しています    
最初のブロック報酬を1とすると、そこから半減期ごとに0.5、0.25、0.125...と減っていきます   
    
なので、    
![image](https://latex.codecogs.com/gif.latex?Reward*%5Csum_%7Bn%3D0%7D%5E%7BN-1%7D%202%5En)    
を計算すれば最後に到達した半減期まで一括で求まってしまいます     
(Reward = 最初のブロック報酬、N = 到達した半減期の回数)    
小数点以下切り捨てしてNを求めると、`N = 508677 / 210000 = 2`となりました    
この場合、`50 * 210000 * 1.5 = 15750000`が出てきます    
    
次に、最後に到達した半減期から今までのブロックまでの報酬ですが、これはそこまで難しくないです     
先に、最後に到達した半減期から今までのブロックまでのブロック数を求めてしまいましょう    
割り算の余り使えば簡単ですね    
`508677 mod 210000 = 88677`が出てきました     
これに今のブロック報酬を掛けます    
`88677 * 12.5 = 1108462.5`になりますね    
    
 これらの値を合計すれば答えが出てきます    
 `15750000 + 1108462.5 = 16858462.5`となります     
     
 では計算機に上から
 
 ```
 210000
 
 508677
 
 50
 ```
 と入力して下さい    
 同じ答えが出ましたね?
