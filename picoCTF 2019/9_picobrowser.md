# picobrowser  

<br>

URL: https://learn.cylabacademy.org/library/9?page=1  

<br>

```
Web Exploitation
Medium
by Archit
picoCTF 2019

This website can be rendered only by picobrowser, go and catch the flag!
```

<br>

## フラグ取得の過程  

「Launch Instance」ボタンを押すことで、追加の詳細が得られる。  
URLが表示されるので、Chromeブラウザーでアクセスする。  

アクセスすると「My New Website」とタイトルされたページが表示され、緑色の大きな「Flag」ボタンがある。  
ボタンを押すと警告のようなメッセージが表示される。  

```
You're not picobrowser! Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36
```

問題文にも書かれているように、picobrowserでないとこのウェブサイトはレンダリングされないことになる。  

そこで、開発者ツールを利用してブラウザーのユーザーエージェントを変更する。  
「Settings」＞「Devices」＞「Add custom device」と進めると、カスタムデバイスの登録とデフォルトデバイスの選択ページが表示される。  
「Add custom device」を選択し、Device欄には適当なデバイス名を、User agent string欄には「picobrowser」と入力する。他の項目はそのままで「Add」ボタンを押して登録する。  
Settingsを閉じて、開発者ツール左上の「Toggle device toolbar」をクリックすることで、画面の様子が変化する。  
上部に「Dimensions: Responsive」の記載があるので、Responsiveを選択して表示されるリストの中からユーザーエージェントを「picobrowser」として登録したデバイスを選択する。  

改めて「Flag」ボタンを押すと、フラグを取得できる。  

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

> picoCTF{p1c0_s3cr3t_ag3nt_fba5c48f}
