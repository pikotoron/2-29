# ループ

## for文

 c言語には何回も繰り返し同じ動作をする繰り返しの文章があり、繰り返す回数が明確に分かっている場合、for文を使います。
 また、繰り返しのことをループといいます。
 for文は、次のような書き方で使用します。

```
int i; //カウント変数
for (初期化;　条件式;　更新) {
繰り返す文;
}
```
この i は整数型の変数であり、繰り返しの回数を数えるために使われます。変数名は何でも構いません。
当然、この i は、for文を使う前に宣言しておく必要があります。
また、このとき使用する変数(int i)を、カウント変数と呼ぶことがあります。
初期化とは、カウント変数の初期化を行うための文です。
条件式とは、ループの終了条件を設定するための文です。
ここに書かれた式の値が真の間は、繰り返す文を実行し続けます。
更新とは、カウント変数の更新を行うための文です。
ここに書かれた式は、繰り返しを行う文を実行した後に実行されます。
 
 次のプログラムは、for文を使用して、メッセージを10回表示する例です。
```
#include <stdio.h>

int main(void)
{
	int i;
	for (i = 0; i < 10; i++) { 
		printf("メッセージ\n");
	}
	return 0;
}
```
このプログラムの実行結果は、次のようになります。
```
メッセージ
メッセージ
メッセージ
メッセージ
メッセージ
メッセージ
メッセージ
メッセージ
メッセージ
メッセージ
```
数えてみると、10回表示されていることがわかります。

このプログラムの動作を説明すると、
変数iが0で初期化され、ループが0で始まります。このとき繰り返す文の一回目が実行されます。
そして、更新が行われ、iが1となり、もう一回ループし、繰り返す文の二回目が実行されます。
この初期化→条件式→繰り返す文→更新→条件式→繰り返す文→更新・・・、という実行を何度も繰り返して、
iが10となったとき、条件式のi<10が偽となり、ループ動作が終了します。

for文は条件式が偽になった時に終了するようにするのが普通ですが、
実は、途中で勝手にfor文を終わらせてしまうことも出来ます。
それには、break文を使用します。

for文の中でbreak文が実行されると、for文は強制的に終了され、
カウント変数はその時点の値のままとなります。
次のプログラムは、break文でループを終了させる例です。
```
#include <stdio.h>

int main(void)
{
	int i;
	for (i = 1;i <= 10;i++) {
		printf("%d\n",i);
		if (i == 3) break;	/* ループを終了する */
	}	return 0;
}
```
このプログラムの実行結果は、次の通りになります。

```
1
2
3
```
条件式を見ると10回表示するまでは終わらないはずなのですが、
3回表示した時点で終了してしまっています。
これは、3回目にiの値が3になり、if文の次のbreak文が実行されたためです。

## while文

for文は、決まった回数だけ繰り返す文でしたが、
それとは逆に、何回繰り返すかわからないときに実行するwhile文があります。
while文は、一般に、次のような書き方で使用します。
```
while (条件式) {
繰り返す文;
}
```
要するに、for文で、条件式しか指定しない場合と同じことなのです。
for文では、初期化と更新が使えるので、定数回ループが簡単に書けるのですが、
ループの回数がわからない場合は、条件式だけのwhile文が便利です。

for文とwhile分の使い分けとして、例えば、
"一か月に５万円貯金する人がいる。四か月貯金をすると合計いくら貯金したことになるか。"
という問題と、
"一か月に５万円貯金する人がいる。３０万円貯金するには何か月貯金すればいいか。"
という問題では、前者はfor文、後者はwhile文を用いると分かりやすいかもしれません。
前者の問題では、貯金をする回数が明確に分かるので、for文で4回繰り返すと貯金の合計が求められます。
後者の問題では、合計が30万円になるまでという条件をwhile文にあてはめ、答えを求められます。

前者のプログラムでは、
```
#include <stdio.h>

int main(void)
{
  int i;
  int money = 0; //変数の初期化
  for(i=0; i<4; i++) { //4カ月貯金している
    money += 5;
    printf("%dか月目、%d万円。\n",i+1,money);
  }
  return 0;
}
```

後者のプログラムでは、
```
#include <stdio.h>

int main(void)
{
  int month = 0;
  int money = 0;
  while (money < 30) { //
    month += 1;
    money += 5;
    printf("%dか月目、%d万円。\n",month,money);
  }
  return 0;
}
```
といった感じです。

# 配列

## 配列とは
配列とは、簡単に言えば一度の宣言でたくさんの変数を宣言することです。
作った配列の変数にはそれぞれ番号があり、番号を参照しながら扱うことで通常の変数のように使うことができます。

例えば、int型の変数Aを100個宣言するとします。
今までの書き方だと、
```
int A1; //変数Aの一個目と考えます。
int A2;
int A3;
   `
   `
   `
```
というように100回繰り返さなければいけません。これは非常にめんどくさいです。
そこで配列を使ってみます。配列を宣言するときは、
```
型名 配列名[要素数];
```
というように宣言します。

型名とは、intやdoubleなどの変数の型のことです。この型の変数が要素数分だけ宣言されます。
配列名とは、そのまま配列の名前です。
要素数とは、配列の中身の変数の数のことです。

これを使って宣言すると、
```
int A[100];
```
これだけで変数が100個宣言されたことになります。


## 配列の扱い
配列を扱うとき、次のように番号をつけて扱います。
```
配列名[番号]
```
このように番号をつけて扱うことを除けば、変数の使い方となんら変わりありません。

例えば、先ほど宣言した配列Aの100個の要素の中の10番目の要素を示すとき、次のようにあらわします。
```
A[9]
```
10番目の要素なんだからA[10]ではないの?と思うかもしれませんが、配列の要素は0番から始まります。要素を100個で宣言したのなら、0~99番までの要素が扱える範囲となります。ここに注意してください。


## 配列と初期化
配列も変数と同様に宣言と同時に値を代入し、初期化することができます。
配列の初期化は次のように行います。
```
型名 配列名[要素数]={0番の数値,1番の数値,2番の数値,・・・};
```

宣言したときの要素数に比べ、代入される数値の個数が少ないとき、代入されていない残りの要素には全て0が代入されます。
配列を初期化して表示する例を示します。
```
#include <stdio.h>

int main(void)
{
	int array[10] = {42,79,13};
	
	printf("array[0] = %d\n",array[0]);
	printf("array[1] = %d\n",array[1]);
	printf("array[2] = %d\n",array[2]);
	printf("array[3] = %d\n",array[3]);
	printf("array[4] = %d\n",array[4]);
	
	return 0;
}
```
このプログラムを実行すると次のようになります。
```
array[0] = 42
array[1] = 79
array[2] = 13
array[3] = 0
array[4] = 0
```

また、要素数を示さずに数値だけを代入すると、要素数を省略できます。
```
#include <stdio.h>

int main(void)
{
	int array[] = {42,79,13};	/* 要素数が省略されている */
	
	printf("array[0] = %d\n",array[0]); //数値の個数分だけ要素が作られる
	printf("array[1] = %d\n",array[1]);
	printf("array[2] = %d\n",array[2]);
	
	return 0;
}
```

## 配列とループ
配列を使うことで、一回の宣言で変数をたくさん確保することができました。しかし、scanfなどでキーボードから数値を読み込み、配列の要素に代入したいとき、
```
scanf("%d %d %d・・・",array[0],array[1],array[2],・・・);
```

というように一つ一つ代入しないといけません。これは非常にめんどくさいですね。
そこで、for文の出番です。for文のループを使うことで、配列を楽に使うことができます。
```
#include <stdio.h>

int main(void)
{
  int i;
  int array[10];
  
  for(i=0; i<10; i++) {
    scanf("%d",&array[i]);
  }

  for(i=0; i<10; i++) {
    printf("array[%d] = %d\n",i,array[i]);
  }

  return 0;
}

```
このように書くことで、10個でも100個でも1000個でも数値の代入を、for文を一回書くだけですませることができます。
これは楽ちんですね。
