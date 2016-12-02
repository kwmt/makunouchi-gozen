# 始め方

```
% git clone git@github.com:kwmt/makunouchi-gozen.git
% cd makunouchi-gozen
// submoduleを同期
% git submodule sync && git submodule update --init && git submodule foreach git pull origin master
// バックグランドでコンテナを起動
% docker-compose up -d
// コンテナに入る
% docker-compose exec web /bin/bash
// アプリの初期設定(vendoringや設定)
# go run tools/init.go 
// アプリをビルドしてhttpサーバーを起動
# bash ./build.sh &
// 確認
// コンテナからだと 9000ポート
% curl -vvv http://localhost:5000
// TODO: 404を確認するのは微妙なので変えたい
* Rebuilt URL to: http://localhost:5000/
*   Trying ::1...
* Connected to localhost (::1) port 5000 (#0)
> GET / HTTP/1.1
> Host: localhost:5000
> User-Agent: curl/7.43.0
> Accept: */*
> 
< HTTP/1.1 404 Not Found
< Content-Type: text/plain
< Date: Fri, 02 Dec 2016 10:32:39 GMT
< Content-Length: 18
< 
* Connection #0 to host localhost left intact
404 page not found
```




* docker-composeで起動したりしたコンテナの状態を確認するには
```
% docker-compose ps
Name              Command               State           Ports         
----------------------------------------------------------------------
db     docker-entrypoint.sh mysqld      Up      3306/tcp              
web    /bin/sh -c /usr/sbin/rsysl ...   Up      0.0.0.0:5000->9000/tcp
```

* docker-compose でスタートしたコンテナをを終了して削除するには
% docker-compose down

### Intellij IDEAで使うためには

1.コンテナのGoソースを `makunouchi-gozen/golang` にコピーする

```
% docker cp web:/usr/local/go/ golang/
```

2.Intellijでmakunouchi-gozenを開く
3.SDKを設定する
	* Project Structure(⌘;)を開いて、Add New SDKでGo SDKを追加する
	* SDKのパスを選択する必要があるので、 `makunouchi-gozen/golang/go/src` を選択します。
4.GOPATHを設定する
	* Configure Go Librariesをクリック
	* GlobalとProjectがありますが、Projectの方で `makunouchi-gozen/gopath` を追加します。

これで補完が効くようになります。


### 開発の流れ

基本的には、  `makunouchi-gozen/gopath/src/gozen` 以下を触ります。
変更したら `docker-compose exec web /bin/bash` でコンテナに入ってるターミナルで、

```
# bash ./build.sh
```

でビルド・実行します。


