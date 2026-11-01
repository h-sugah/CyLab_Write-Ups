# mus1c

<br>

URL: https://learn.cylabacademy.org/library/15

<br>

```
General Skills
Medium
by Danny
picoCTF 2019

I wrote you a song. Put it in the academy{} flag format.
```

<br>

## フラグ取得の過程  

「song」のリンクを選択するとファイルをダウンロードすることができる。

ファイル名は「mus1c-lyrics.txt」のテキストファイルである。

エディターで内容を確認する。

Picoと叫びながらセキュリティの重要性を訴える歌詞になっている。

これをどのように扱っていけば検討がつかないのでヒントを参照すると、「Do you think you can master rockstar?」と書かれている。

rockstarについて検索すると、プログラミング言語として存在していることが分かる。

https://codewithrockstar.com/

このサイトでは、オンラインで実行する環境も用意されていた。

https://codewithrockstar.com/online

上記サイトに、ダウンロードしたrockstarのコードをコピー＆ペーストして「Rock」ボタンを押したところ、以下のような出力が得られた。

```
114
114
114
111
99
107
110
114
110
48
49
49
51
114
```

この数値をasciiコードとしてデコードすることでフラグになる。

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## フラグ  

> academy{rrrocknrn0113r}
