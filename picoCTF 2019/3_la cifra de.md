# la cifra de  

URL: https://learn.cylabacademy.org/library/3  

```
Cryptography
Medium
200 pts
by Alex Fulton/Daniel Tunitis
picoCTF 2019

I found this cipher in an old book.
```

## フラグ取得の過程  

インスタンスを起動するボタンがあり、インスタンスを起動すると、追加の詳細が表示される。  
追加の詳細は、以下の問題文の続きとリモートアクセス先の情報だった。  

```
Can you figure out what it says? Connect with nc ＜アクセス先情報＞.
```

アクセスすると、以下の情報が出力された。  

```
$ nc ＜アクセス先情報＞
Encrypted message:
Ne iy nytkwpsznyg nth it mtsztcy vjzprj zfzjy rkhpibj nrkitt ltc tnnygy ysee itd tte cxjltk

Ifrosr tnj noawde uk siyyzre, yse Bnretèwp Cousex mls hjpn xjtnbjytki xatd eisjd

Iz bls lfwskqj azycihzeej yz Brftsk ip Volpnèxj ls oy hay tcimnyarqj dkxnrogpd os 1553 my Mnzvgs Mazytszf Merqlsu ny hox moup Wa inqrg ipl. Ynr. Gotgat Gltzndtg Gplrfdo 

Ltc tnj tmvqpmkseaznzn uk ehox nivmpr g ylbrj ts ltcmki my yqtdosr tnj wocjc hgqq ol fy oxitngwj arusahje fuw ln guaaxjytrd catizm tzxbkw zf vqlckx hizm ceyupcz yz tnj fpvjc hgqqpohzCZK{m311a50_0x_a1rn3x3_h1ah3ximdI91f3}

Ehk ktryy herq-ooizxetypd jjdcxnatoty ol f aordllvmlbkytc inahkw socjgex, bls sfoe gwzuti 1467 my Rjzn Hfetoxea Gqmexyt.

Tnj Gimjyèrk Htpnjc iy ysexjqoxj dosjeisjd cgqwej yse Gqmexyt Doxn ox Fwbkwei Inahkw.

Tn 1508, Ptsatsps Zwttnjxiax tnbjytki ehk xz-cgqwej ylbaql rkhea (g rltxni ol xsilypd gqahggpty) ysaz bzuri wazjc bk f nroytcgq nosuznkse ol yse Bnretèwp Cousex.

Gplrfdo’y xpcuso butvlky lpvjlrki tn 1555 gx l cuseitzltoty ol yse lncsz. Yse rthex mllbjd ol yse gqahggpty fce tth snnqtki cemzwaxqj, bay ehk fwpnfmezx lnj yse osoed qptzjcs gwp mocpd hd xegsd ol f xnkrznoh vee usrgxp, wnnnh ify bk itfljcety hizm paim noxwpsvtydkse.
```

出力された情報を見ると、中央部分にフラグのような文字列を確認できる。  

> hgqqpohzCZK{m311a50_0x_a1rn3x3_h1ah3ximdI91f3}  

先頭の4文字が不明だが「pohzCZK{・・・}」の部分が「picoCTF{・・・}」になると推測できる。  
フラグのフォーマットを把握できるので、換字式暗号を使っていると想定する。  
CyberChefを使用して変換を試みる。  
ROT13のレシピでブルートフォースなどを試してみたが、特にフラグになるような文字列が得られなかった。  
そこで、ヴィジュネル暗号とを使っているのではないかと考えて変換を試みる。  
1文字目がpで、5文字目がCになっており、4文字の周期性がある。  
これで、暗号キーは4文字だと判断できる。  
Vigenere Decodeのレシピを利用し、1文字ずつ入力して文字列の変化を確認していくと、キーが「agfl」で以下のような文字列になった。  

CyberChef: https://gchq.github.io/CyberChef/  

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

> picoCTF{b311a50_0r_v1gn3r3_c1ph3rdbdC91a3}  
