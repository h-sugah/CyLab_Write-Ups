# vault-door-1

<br>

URL: https://learn.cylabacademy.org/library/12

<br>

```
Reverse Engineering
Medium
by Mark E. Haase
picoCTF 2019

This vault uses some complicated arrays! I hope you can make sense of it, special agent. The source code for this vault is here: VaultDoor1.java
```

<br>

## フラグ取得の過程  

VaultDoor1.javaのリンクをクリックすると、同名のファイルをダウンロードすることができます。

拡張子がjavaのソースコードなので、エディターで開きます。

問題文にも書いてある通り、配列が記述されています。

ソースコードを読むと、動作は次のようになっています。
- main()でフラグになるパスワードを入力させ、inputにセットしています。
- inputを引数にしてcheckPassword()を呼び出します。
- checkPassword()では、受け取ったパスワードの文字数と、charAt()メソッドのインデックスの文字が指定された文字と一致しているかをチェックしています。
- &&の論理演算で接続されているので、条件を全部満たすことでアクセスを獲得できます。

これにより、checkPassword()の条件を判断しているcharAt()メソッドのインデックスを順番に並べることでパスワードになり、それがフラグであることが分かります。

checkPassword()で文字を判定している部分で、インデックスを昇順に並べ替えると、以下のようになります。
```
password.length() == 32 &&
password.charAt(0)  == 'd' &&
password.charAt(1)  == '3' &&
password.charAt(2)  == '5' &&
password.charAt(3)  == 'c' &&
password.charAt(4)  == 'r' &&
password.charAt(5)  == '4' &&
password.charAt(6)  == 'm' &&
password.charAt(7)  == 'b' &&
password.charAt(8)  == 'l' &&
password.charAt(9)  == '3' &&
password.charAt(10) == '_' &&
password.charAt(11) == 't' &&
password.charAt(12) == 'H' &&
password.charAt(13) == '3' &&
password.charAt(14) == '_' &&
password.charAt(15) == 'c' &&
password.charAt(16) == 'H' &&
password.charAt(17) == '4' &&
password.charAt(18) == 'r' &&
password.charAt(19) == '4' &&
password.charAt(20) == 'c' &&
password.charAt(21) == 'T' &&
password.charAt(22) == '3' &&
password.charAt(23) == 'r' &&
password.charAt(24) == '5' &&
password.charAt(25) == '_' &&
password.charAt(26) == 'e' &&
password.charAt(27) == '3' &&
password.charAt(28) == 'f' &&
password.charAt(29) == 'f' &&
password.charAt(30) == '6' &&
password.charAt(31) == '3';
```

各文字を繋げて、所定のフォーマットにすることでフラグになります。

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

> academy{d35cr4mbl3_tH3_cH4r4cT3r5_e3ff63}
