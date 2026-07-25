# where are the robots  

<br>

URL: https://learn.cylabacademy.org/library/4  

<br>

```
Web Exploitation
Easy
100 pts
by zaratec/Danny
picoCTF 2019

Can you find the robots?
```

<br>

## フラグ取得の過程  

インスタンスを起動するボタンがあり、インスタンスを起動すると、追加の詳細が表示される。  

追加の詳細は、アクセス先のURLだった。  

URLへアクセスすると、シンプルなWelcomeページが表示される。  

そのページには、「Where are the robots?」と記述されている。  

robotsを見つけろ、ということなので、robots.txtを参照する。  

ブラウザーのURL入力欄に、現在のURLに追加して「/robots.txt」を入力してアクセスする。  

robots.txtの内容が表示される。  

```
User-agent: *
Disallow: /cc6b1.html
```

/cc6b1.htmlにアクセスするとフラグを取得できる。  

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

> picoCTF{ca1cu1at1ng_Mach1n3s_cc6b1}  
