# 覚えてないもの一覧
* `gpg -e -r user@ping-t.com hoge` ファイルは最後。ユーザーの前に -r が必要。
* `gpg --import pubkey` -ではなく--
* `gpg --sign hoge` -ではなく--
* `gpg --gen-key` gpg-keygen ではない
* `ssh -o IdentityFile` IdentifyFile ではない
* `ifconfig` => `ip addr`
* `route` => `ip route`
* `netstat` => `ss`
* `whois` ドメイン登録者の情報
* `host -t mx example.com`
* `dig -t ns yahoo.co.jp`
* `dig yahoo.co.jp ns`
* `dig yahoo.co.jp any`
    - a, mx, ns, any, txt, soa
* `dig @8.8.8.8 yahoo.co.jp`
* `/etc/cups/cupsd.conf`
* `~/.forward` 自分宛てのメールの転送先
* `newaliases` `/etc/aliases` を編集した後に反映させるコマンド
* `/var/log/journal/` systemd-journald のログを永続的に保存させる場所
* `journalctl --vacuum-time` 指定した期間より古いアーカイブジャーナルを削除する
* `timedatectl set-time "2019-05-01 15:30:27"` set-time を抜かないように
* `hwclock --systohc` -ではなく--である。--hctosysも同じ。


# シェル

## Q
* profile, .bash_login, bashrc のうち、ログインシェルにより一度だけ読み込まれるものは？そうでないほうはいつ読み込まれる？
* profile, .bash_login, bashrc を読み込む順番
.  
.  
.  
.  

## A
* profile, .bash_login はログインシェルにより一度だけ読み込まれる。bashrc は非ログインシェルの起動のたびに読み込まれる。
* 順番
    - `/etc/profile`
    - `~/.bash_profile`, `~/bash_login`, `~/.profile` の順に探していずれかを読む
    - `~/.bashrc`
    - `/etc/bashrc`

## Q
* コマンドの実行結果をシェル変数に入れる方法2種類
* 算術演算を使用する
.  
.  
.  
.  

## A
* `$(command)` または ``command`` シングルクォートでコマンドをくくる
* `$((1+2))`

## Q
* 子シェルで実行する方法
* 現在のシェルで実行する方法
.  
.  
.  
.  

## A
* `bash ./myshell.sh`, `./myshell.sh`
* `source ./myshell.sh`, `. ./myshell.sh`, function を使う


## Q
* declare のオプション
    - -p
    - -i
    - -r
    - -f
.  
.  
.  
.  

## A
* declare のオプション
    - -p 変数の属性と中身を確認。-i や -r で属性をつけてから -p で確認すると属性がわかる。
    - -i 整数のみ入れられるようにする。文字列を入れると0になる。
    - -r readonlyにする。代入できなくなる。
    - -f 現在のシェルで使える関数を表示する

## Q
* bash の組み込みコマンド(例: declare, read, alias, cd)の使い方の調べ方
.  
.  
.  
.  

## A
* `bash -c "help コマンド名`
    - `bash -c help declare`

## Q
* alias を設定する方法
* alias を解除する方法
* alias を一時解除する方法
* alias を引数なしで実行したとき
.  
.  
.  
.  

## A
* `alias ls='ls -la --color=auto'`
* `unalias ls`
* `\ls`
* すべてのエイリアスが表示される

## Q
* 特殊なシェル変数
    - シェルのPID
    - 最後に実行したコマンドの終了値
    - 引数の個数
    - 区切り文字(デフォルト空白)で区切られたすべての引数
    - 実行ファイル名
    - 1番目の引数
* 2つの引数を参照するスクリプト `echo $1 $2` が実行されたとき
    - 引数が1つしか指定されなかったら？
    - 引数が3つ以上指定されたら？
* 10番目の引数を表す方法
.  
.  
.  
.  
## A
* 特殊なシェル変数
    - `$$` シェルのPID
    - `$?` 最後に実行したコマンドの終了値 (正常なら0)
    - `$#` 引数の個数
    - `$*` 区切り文字(デフォルト空白)で区切られたすべての引数
    - `$0` 実行ファイル名
    - `$1` 1番目の引数
* 2つの引数を参照するスクリプト `echo $1 $2` が実行されたとき
    - `$1` が表示されるだけ
    - `$1 $2` が表示されるだけ
* `${10}`
    - `$10` と書いたら、`$1` に 0 をつけたものと解釈される。

## Q
* if 文での条件式の書き方2種類
* パスに関する条件式
* ファイルの更新日に関する条件式
* 文字列の長さに関する条件式
* 比較演算子は整数と文字列で異なる。`=`, `==`, `!=` を使うのはどちらか？ `-eq`, `-ne` を使うのはどちらか？
.  
.  
.  
.  
## A
* `if test 条件式` あるいは `if [ 条件式 ]`
* パスに関する条件式
    - -d ディレクトリなら真
    - -e ファイルまたはディレクトリが存在すれば真
    - -f 通常ファイルが存在すれば真。ブロックデバイスファイル(例: `/dev/sda1`)は通常ファイルではない。
    - -r 読み込み可能なファイルが存在すれば真
    - -w 書き込み可能なファイルが存在すれば真
    - -x 実行可能なファイルが存在すれば真
    - -L シンボリックリンクであれば真
* ファイルの更新日に関する条件式
    - -nt Newer than
    - -ot Older than
* 文字列の長さに関する条件式
    - -n 0より大きければ真
    - -z 0であれば真
* 文字列では `=`, `==`, `!=` を使う。整数では `-eq`, `-ne` を使う。

## Q
* `seq 3`
* `seq 98 100`
* `seq 3 5 14`
.  
.  
.  
.  
## A
* `seq 3`
```
1
2
3
```

* `seq 98 100`
```
98
99
100
```

* `seq 3 5 14`
```
3
8
13
```

## Q
* set の `-o`, `+o` オプションはどちらが有効化、無効化か
* set のオプション
    - allexport
    - emacs
    - ignoreeof
    - noclobber
    - noglob
    - noexec
    - vi
* `set -o` のオプションを指定しなかった場合
.  
.  
.  
.  
## A
* `-o` が有効化。`+o` が無効化。
* set のオプション
    - allexport: 新規作成・変更した変数を自動的に環境変数とする
    - emacs: emacsと同じキーバインドにする 
    - ignoreeof: Ctrl+Dを押してもログアウトしないようにする
    - noclobber: リダイレクトしたときファイルを上書きできないようにする
    - noglob: ワイルドカード `*, ? など` による展開を無効にする
    - noexec: シェルスクリプトを実行しようとしたときに実行せず、構文エラーをチェックするのみとする
    - vi: viと同じキーバインドにする
* 各オプションの on/off が表示される

## Q
* 何も環境変数が設定されていない状態にする方法
* 指定した環境変数を一時的に削除する方法
* 指定した環境変数を削除する方法
.  
.  
.  
.  
## A
* `env -i`
* `env -u 環境変数名`
* `unset 環境変数名`

## Q
* case文の書式
.  
.  
.  
.  
## A
```
case $1 in
    1) echo "one" ;;
    2) echo "two" ;;
    3) echo "three" ;;
esac
```

# X Window System

## Q
* X.Orgの設定ファイルパス
* 設定ファイルの項目
.  
.  
.  
.  
## A
* `/etc/X11/xorg.conf`, `/etc/X11/xorg.conf.d/`
* 設定ファイルの項目
    - ServerLayout 入出力デバイスの組み合わせとスクリーン
    - Files フォント関連のパス
    - Module Xサーバーが読み込むダイナミックモジュール
    - InputDevice Xサーバーに対するキーボードやマウスなどの入力デバイス
    - Monitor 垂直、水平周波数
    - Device ビデオカードのドライバ名
    - Screen 解像度と色深度

## Q
* Xサーバーへのリモートアクセスを制御する方法
.  
.  
.  
.  
## A
* xhost コマンド
    - `+ホスト名` 許可する
    - `-ホスト名` 拒否する
    - `+` すべてのホストを許可
    - `-` すべてのホストを拒否

## Q
DISPLAY 変数の書式
.  
.  
.  
.  

## A
* `サーバー名:ディスプレイ番号.スクリーン番号`
    - 例 `localhost:0.0`, `localhost:0.1`
    - localhostは省略できる。`:0.0`
    - ディスプレイ番号は、同じキーボードとマウスを共有するモニタの集合に対してつけられる。0から始まる。多くの場合0しかない。
    - スクリーン番号はモニタにつけられる番号。0から始まる。モニタが2台あるとき、0, 1となる。


## Q
* ディスプレイマネージャーの起動
.  
.  
.  
.  

## A
* systemd の場合
    - systemd がシンボリックリンク display-manager.service の指すディスプレイマネージャー起動ユニット(例: /usr/lib/systemd/system/kdm.service)を起動
    - 事前に `systemctl enable kdm` として設定しておく
* SysV init の場合
    - prefdm(preffered display manager) がディスプレイマネージャー X Window System:xdm , GNOME:gdm, KDE:kdm or sddm, ... を起動

## Q
ランレベル3から startx する処理
.  
.  
.  
.  

## A
* startx
* xinit
* `~/.xinitrc` なければ `/etc/X11/xinit/xinitrc`
* ウィンドウマネージャー起動

## Q
* `/etc/X11/xdm/` にあるファイル
.  
.  
.  
.  

## A
* xdm-config: 設定ファイル
* Xresources: XDMログイン画面のデザイン
* Xaccess: ホストからXDMへのアクセス許可
* Xsetup_0: ログイン画面表示前に実行されるスクリプト
* Xsession: ログイン後に実行されるスクリプト

## Q
* Xで利用可能な色とRGB値の情報確認
* 実行中のXクライアントを表示
* ディスプレイ番号、スクリーン番号、解像度を表示
.  
.  
.  
.  

## A
* showrgb: Xで利用可能な色とRGB値の情報確認
* xlsclients: 実行中のXクライアントを表示
* xdpyinfo: ディスプレイ番号、スクリーン番号、解像度を表示


## Q
* キーボードアクセシビリティ
    - スティッキーキー
    - スローキー
    - バウンスキー
    - トグルキー
    - マウスキー
    - リピートキー
.  
.  
.  
.  

## A
* キーボードアクセシビリティ
    - スティッキーキー: Ctrl, Alt, Shift などの修飾キーの後に入力したキーを同時押しとみなす。2つ以上のキーを同時に押せないユーザー向け。
    - スローキー: 通常よりも長い一定時間キーを押し続けると入力とみなす。正確にキーを押すことが難しいユーザー向け。
    - バウンスキー: 同じキー入力を一定時間無視する。意図せず何度も同じキーを押してしまうユーザー向け。
    - トグルキー: NumLock, CapsLock, ScrollLockキーがonだと1回、offだと2回ビープ音が鳴る。各キーのLEDが見えないユーザー向け。
    - マウスキー: マウスの代わりにテンキーで操作する。マウスを使いづらいユーザー向け。
    - リピートキー: 入力リピートするのに必要な時間を通常よりも長くする。キーを押した後すぐに指を離せないユーザー向け。

## Q
* オンスクリーンキーボードの例
* 拡大鏡の例
* スクリーンリーダーの例
.  
.  
.  
.  

## A
* gok (GNOME2), GNOME Shell (GNOME3)
* orca (GNOME2), GNOME Shell (GNOME3)
* emacspeak (Emacsに読み込んだテキストやメールを音声で読み上げる)

# 管理タスク - アカウント

## Q
* `/etc/passwd` の書式

.  
.  
.  
.  

## A
* ログイン名
* x または 暗号化パスワード
* UID
* GID (プライマリ)
* コメント
* ホームディレクトリ
* ログインシェル


## Q
* `/etc/group` の書式

.  
.  
.  
.  

## A
* グループ名
* グループパスワード
* GID
* 補助グループとして参加しているユーザーのリスト

## Q
* `/etc/shadow` の書式

.  
.  
.  
.  

## A
* ユーザー名
* パスワード
* 日数1～6

## Q
* ユーザーのパスワードを変更するコマンド
* パスワードの有効期限を変更するコマンド
* ユーザーを新規作成するコマンド
* ユーザーを削除するコマンド
* 既存ユーザーの設定を変更するコマンド
* グループを新規作成するコマンド
* グループを削除するコマンド
* 既存グループの設定を変更するコマンド
* ユーザーのUIDやGIDを表示するコマンド
* ユーザーの所属するグループを表示するコマンド
* グループのパスワードやメンバーを設定するコマンド

.  
.  
.  
.  

## A
* passwd ユーザーのパスワードを変更するコマンド
* chage パスワードの有効期限を変更するコマンド
* useradd ユーザーを新規作成するコマンド
* userdel ユーザーを削除するコマンド
* usermod 既存ユーザーの設定を変更するコマンド
* groupadd グループを新規作成するコマンド
* groupdel グループを削除するコマンド
* groupmod n既存グループの設定を変更するコマンド
* id ユーザーのUIDやGIDを表示するコマンド
* groups ユーザーの所属するグループを表示するコマンド
* gpasswd グループのパスワードやメンバーを設定するコマンド



## Q
* useradd でオプションを指定しなかったときのデフォルト値が定められているファイルパス
* useradd のオプション
    - -c
    - -d
    - -e
    - -f
    - -g
    - -G
    - -k
    - -m
    - -M
    - -s
    - -u
    - -D

.  
.  
.  
.  

## A
* `/etc/default/useradd`
* useradd のオプション
    - -c コメント
    - -d ホームディレクトリの指定
    - -e 失効日
    - -f 失効～使用不能までの日数
    - -g 1次グループ
    - -G 2次グループ
    - -k skelディレクトリ
    - -m ホームディレクトリの作成
    - -M ホームディレクトリを作成しない
    - -s ログインシェルの指定
    - -u UIDの指定
    - -D デフォルト値の表示あるいは設定

## Q
* usermod のオプション
    - -d
    - -g
    - -G
    - -s
    - -L
    - -U
    - -p

.  
.  
.  
.  

## A
* usermod のオプション
    - -d ホームディレクトリを指定
    - -g プライマリグループを指定
    - -G 補助グループを指定
    - -s ログインシェルを指定
    - -L パスワードをロックする
    - -U パスワードをアンロックする
    - -p 暗号化済のパスワードを設定する

## Q
* userdel のオプション
.  
.  
.  
.  

## A
* userdel のオプション
    - -r ホームディレクトリも削除
    - -f ユーザーがログイン中でも削除

## Q
* groupmod のオプション
    - -g
    - -n

.  
.  
.  
.  

## A
* groupmod のオプション
    - -g GIDを変更
    - -n グループ名を変更



## Q
* passwd のオプション
    - -l
    - -u
.  
.  
.  
.  

## A
* passwd のオプション
    - -l パスワードをロックする
    - -u パスワードをアンロックする

## Q
* chage の書式
* chage のオプション
    - -l
    - -d
    - -m
    - -M
    - -W
    - -I
    - -E
.  
.  
.  
.  

## A
* `chage [オプション 引数] ユーザー名`
* chage のオプション
    - -l ユーザーの情報
    - -d パスワード最終更新日を設定
    - -m パスワード更新間隔の最短日数
    - -M パスワード更新せずに使用できる最長日数
    - -W パスワード変更期限の何日前から警告を出すか
    - -I パスワードの変更期限を過ぎてからアカウントが使用できなくなるまでの猶予日数
    - -E アカウントの失効日を設定


## Q
* id コマンドのオプション
    - -u
    - -g
    - -G
.  
.  
.  
.  

## A
* id コマンドのオプション
    - -u 指定ユーザー名のUIDを表示
    - -g 指定ユーザー名のプライマリGIDを表示
    - -G 指定ユーザー名の参加する全GIDを表示


# 管理タスク - ジョブスケジューリング

## Q
* crontab を監視するデーモンと監視周期
* crontab 設定ファイルの書式
* crontab 設定ファイルの在り処 (システム用、ユーザー用)
* crontab コマンドオプション
    - 編集
    - 内容表示
    - crontabファイル削除
* cron を利用するユーザーを制限する方法
.  
.  
.  
.  

## A
* crond が1分ごとに起動し、crontab を調べてジョブを実行する
* crontab の書式
    * `分 時 日 月 曜日 コマンド`
        - 1行1エントリ
        - `*` 問わない場合(例：毎日1:00実行なら日と月と曜日はは `*` でよい)
        - 範囲指定: 15-17(15,16,17時それぞれ)、1-4(月曜から木曜)
        - リスト指定:
        - 間隔指定: 分に 10-20/2 を指定すると 10分から20分の間で2分間隔で実行。時に1、分に `*/15` を指定すると、1:00, 1:15, 1:30, 1:45に実行される。
        - 曜日: 0 Sunday - 6 Saturday または sun,mon,tue,wed,thu,fri,sat どちらか
* crontab の在り処
    - システム用 `/etc/crontab`
    - ユーザー用 `/var/spool/cron/ユーザー名`
* crontab コマンドオプション
    - -e 編集
    - -l 内容表示
    - -r crontabファイル削除
* cron を利用するユーザーを制限する方法
    - `/etc/cron.allow` だけがある場合、載っているユーザーだけが利用できる
    - `/etc/cron.deny` だけがある場合、載っていないユーザーだけが利用できる
    - 両方ない場合、CentOSならrootだけ、Ubuntuなら全ユーザーが利用できる
    - 両方ある場合、`/etc/cron.deny` は無視され、`/etc/cron.allow` に載っているユーザーだけが利用できる

## Q
* システム用 crontab はユーザー用と何が異なるか
.  
.  
.  
.  

## A
* SHELL, PATH, MAILTO, HOME が書いてある
* その後にユーザー用と同様に実行周期を記述したエントリが続き、毎時 `/etc/cron.hourly`、毎日`/etc/cron.daily`、毎週`/etc/cron.weekly`、毎月`/etc/cron.monthly` が記述されている。
* ユーザー用のエントリに加え、実行ユーザーが加わる。
* サービス個別のジョブ実行の定義は `/etc/cron.d/` に置かれる

## Q
* systemd のタイマーユニットを有効にして開始する方法
* 有効なタイマーの一覧表示方法
* タイマーユニットの在り処
* タイマーユニットの記述例
.  
.  
.  
.  

## A
* `systemctl enable my-routine.timer`, `systemctl start my-routine.timer`
* `systemctl list-timers`
* `/etc/systemd/system/my-routine.timer`

monotonic timer の場合。
```
[Timer]
OnActiveSec=1hour
OnUnitActiveSec=1hour
Unit=my-routine.service
```

OnActiveSec (タイマーをアクティベートしてからの時間) 以外に OnBootSec (マシンが起動した後の時間) もある。


realtime timer の場合。
```
[Timer]
OnCalendar=*-*-* 3:00:00
Unit=my-routine.service
```

OnCalendar の書式は、`Day-of-week YYYY-MM-DD hh:mm:ss` であり、曜日、年-月-日は省略可能。


## Q
* OnCalendar の書式いろいろ
* 毎週月曜0:00
* 毎週月曜0:00と水曜0:00
* 毎日15時
* 毎週月曜15:00
.  
.  
.  
.  

## A
* `Day-of-week YYYY-MM-DD hh:mm:ss`
* `Mon`
* `Mon,Wed`
* `15:00`
* `Mon 15:00` または `Mon *-*-* 15:00:00`

# 管理タスク - ロケールとタイムゾーン

## Q
* ロケールの設定ファイル
* ロケールの環境変数
    - LANG
    - LC_TIME
    - LC_CTYPE
    - LC_MESSAGES
    - LC_ALL
.  
.  
.  
.  

## A
* `/etc/locale.conf`
* ロケールの環境変数
    - LC_TIME 日付と時刻の書式
    - LC_CTYPE 文字の種類
    - LC_MESSAGES 出力メッセージの言語
    - LC_ALL すべての `LC_*` を上書きする。非推奨。
    - LANG: すべての `LC_*` を上書きするが、カテゴリ毎の設定が可能。`LANG=ja_JP.utf8`

## Q
* 国や地域ごとのタイムゾーン情報がバイナリファイルとして保存されているパス
* システムのタイムゾーンを示すバイナリファイル
* システムのタイムゾーンを示すテキストファイル
.  
.  
.  
.  

## A
* `/usr/share/zoneinfo/`
* `/etc/localtime`
* `/etc/timezone`

```
$ file /etc/localtime
/etc/localtime: symbolic link to /usr/share/zoneinfo/Asia/Tokyo
```

## Q
* tzconfig とは
* tzselect とは
.  
.  
.  
.  

## A
* tzconfig: `/etc/localtime`, `/etc/timezone` の両方を設定するコマンド。
* tzselect: 環境変数TZや `/etc/timezone` で指定する値を確認するためのコマンド。

# 必須システムサービス - 時刻

## Q
* date コマンドで時刻を設定するときの書式
.  
.  
.  
.  

## A
* `date MMDDhhmmCCYY.ss`
* `date MMDDhhmmYY` .ss と CC は省略可能。
* `date MMDDhhmm` 現在と同じ年であれば YY は省略可能。

## Q
* timedatectl のサブコマンド
    - 現在の日付時刻や状態の表示
    - NTPによる時刻同期の有効/無効
    - 日付や時刻の設定
    - タイムゾーンの設定
    - タイムゾーンの一覧表示
.  
.  
.  
.  

## A
* timedatectl のサブコマンド
    - status (デフォルト)
    - set-ntp yes | no
    - set-time CCYY-MM-DD hh:mm:ss (または CCYY-MM-DD のみ、または hh:mm:ss のみ)
    - set-timezone タイムゾーン
    - list-timezones



## Q
* ntpq コマンドの引数とオプション
.  
.  
.  
.  

## A
* ntpq コマンドの引数とオプション
    - -p 引数に指定したサーバーとの同期状態を表示。引数がなければ ntpd の設定ファイルパスにあるNTPサーバー群との同期状態を表示。
    - -i 引数がないと対話モードで起動（デフォルト）


## Q
* ntpd の設定ファイルパスは何か？何が書かれているか？
.  
.  
.  
.  

## A
* `/etc/ntp.conf`
    - server: NTPサーバーの指定の書式で書かれている
    - driftfile: 参照時刻からのずれを記録するファイルパス `/var/lib/ntp/drift`


## Q
* chrony の設定ファイルパスは何か？何を指定できるか？
.  
.  
.  
.  

## A
* `/etc/chrony.conf`
    - server: NTPサーバーの指定
        - サーバーの後に iburst をつけると時刻問い合わせ周期を短くする
    - peer: 同じstratumのNTPサーバーを指定
    - pool: 複数のNTPサーバーのアドレスを集約した名前を指定
    - driftfile: 自身の時刻のずれを記録するファイルを指定
    - rtcsync: システムクロックをハードウェアクロックにコピーする


## Q
* chronyc のサブコマンド
    - オンライン/オフラインのNTPサーバー数
    - 時刻のソース
    - 時刻のソースの統計情報
    - 時刻同期の詳細情報
.  
.  
.  
.  

## A
* chronyc のサブコマンド
    - activity
    - sources
    - sourcestats
    - tracking


# 必須システムサービス - ロギング

## Q
* syslog や systemd-journal の設定ファイルでファシリティとプライオリティを指定するときの書式
* ファシリティ一覧
* プライオリティ一覧
.  
.  
.  
.  

## A
* syslog や systemd-journal の設定ファイルでファシリティとプライオリティを指定するときの書式
    - `ファシリティ.プライオリティ`, ファシリティとプライオリティそれぞれがなんでもいいときは `*` (例: `*.emerg`)
* ファシリティ一覧
    - kern
    - user
    - mail
    - daemon
    - auth
    - syslog
    - lpr
    - news
    - uucp
    - cron
    - authpriv
    - ftp
    - local0～local7
* プライオリティ一覧
    - emerg
    - alert
    - crit
    - err
    - warning
    - info
    - debug
    - none


## Q
* journalctl コマンドのオプション
    - 最新部分までジャンプして表示
    - リアルタイムに表示
    - 表示行数を指定
    - 指定したプライオリティのログを表示
    - 逆順に表示（最新のものを最上位に）
    - 指定日時以降を表示
    - 指定日時以前を表示
    - 指定期間分を残して削除
    - 指定サイズ分を残して削除
.  
.  
.  
.  

## A
* journalctl コマンドのオプション
    - -e, --pager-end: 最新部分までジャンプして表示
    - -f, --follow: リアルタイムに表示
    - -n, --lines: 表示行数を指定
    - -p, --priority: 指定したプライオリティのログを表示
    - -r, --reverse: 逆順に表示（最新のものを最上位に）
    - --since: 指定日時以降を表示
    - --until: 指定日時以前を表示
    - --vacuum-time: 指定期間分を残して削除
    - --vacuum-size: 指定サイズ分を残して削除


## Q
* 任意のファシリティとプライオリティとメッセージを指定してログに記録するコマンド
* コマンドの実行結果を systemd-journal に送ってログに記録するコマンド
.  
.  
.  
.  

## A
* `logger -p user.info "Message"`
* `systemd-cat コマンド`

# 必須システムサービス - プリンタ

## Q
* lpr
* lprm
* lpq
* 上記どれかで印刷する方法
* すべての印刷ジョブを削除する方法
.  
.  
.  
.  

## A
* 印刷ジョブをプリントキューに登録
* プリントキューにある印刷ジョブを削除 `lprm -Pプリンタ名 ジョブ番号`
* プリントキューにある印刷ジョブを表示
* `lpr -Pプリンタ名 印刷するファイル名`
* `lprm -Pプリンタ名 -`

## Q
* CUPS の特徴
* CUPS デーモンの設定ファイル
* CUPS にてプリンタの共有設定をするファイル
* 印刷ジョブを生成しプリントキューに登録するコマンド
* プリントキューにある印刷ジョブを削除するコマンド
* プリントキューにある印刷ジョブを表示するコマンド
.  
.  
.  
.  

## A
* 印刷プロトコルがIPP(Internet Prinrint Protocol)、PPDをサポート、lpdと互換あり、Webブラウザから設定可能(631ポート)
* `/etc/cups/cupsd.conf`
* `/etc/cups/printers.conf`
* lp
* cancel
* lpstat

# ネットワークの基礎

## Q
* IPv4 アドレスの1バイト目が示すクラスの境界
.  
.  
.  
.  

## A
* A: 0～127
* B: 128～191
* C: 192～223
* D: 224～239
* E: 240～255

## Q
* IPv6 ユニキャストアドレス
    - グローバルユニキャストアドレス
    - ユニークローカルユニキャストアドレス
    - リンクローカルアドレス
* IPv6 アドレス 後ろ半分の長さと呼び名
.  
.  
.  
.  

## A
* Ipv6 ユニキャストアドレス
    - グローバルユニキャストアドレス: 200 から始まる
    - ユニークローカルユニキャストアドレス: FC00 から始まる
    - リンクローカルアドレス: FE80 から始まる
* インターフェースID（インターフェース識別子）、64bit


## Q
* ポート名とサービスの対応が書かれたファイル
* IPアドレスとホスト名の対応が書かれたファイル
* 名前解決やサービス名解決の際の問い合わせ順序を指定するファイル。およびそのファイルを参照して問い合わせをするコマンド。
* ドメイン名やDNSサーバーを指定するファイル
* ホスト名を設定するファイル

.  
.  
.  
.  

## A
* `/etc/services`
* `/etc/hosts`
* `/etc/nsswitch.conf`, `getent`
* `/etc/resolv.conf` (resolve ではないことに注意)
* `/etc/hostname`

## Q
* netstat コマンドのオプション
    - ルーティングテーブルを表示
    - 統計情報を表示
    - 接続待ちソケットを表示
    - TCPソケットを表示
    - UDPソケットを表示
    - UNIXソケットを表示
    - TCP,UDP,UNIXすべてのソケットを表示
    - ホスト、ポート、ユーザーの名前を解決せず数字で表示
.  
.  
.  
.  

## A
* netstat コマンドのオプション
    - -r, --route ルーティングテーブルを表示
    - -s, --statistics 統計情報を表示
    - -l, --listening 接続待ちソケットを表示
    - -t, --tcp TCPソケットを表示
    - -u, --udp UDPソケットを表示
    - -x, --unix UNIXソケットを表示
    - -a, --all TCP,UDP,UNIXすべてのソケットを表示
    - -n, --numeric ホスト、ポート、ユーザーの名前を解決せず数字で表示

## Q
* nmcli コマンドのオブジェクトに対して何ができるか
    - general
    - networking
    - radio
    - connection
    - device
.  
.  
.  
.  

## A
* nmcli コマンドのオブジェクトに対して何ができるか
    - general status: Network Manager の状態を表示
    - general hostname: ホスト名を表示
    - general hostname ホスト名: 指定したホスト名に変更
    - networking on: ネットワークを有効化
    - networking off: ネットワークを無効化
    - radio wifi: WiFi状態を表示
    - radio wifi on: WiFi有効化
    - radio wifi off: WiFi無効化
    - connection show: 接続状況を表示
    - connection up 接続ID: 接続有効化
    - connection down 接続ID: 接続無効化
    - connection modify
    - device status: デバイスの状態を表示
    - device show インターフェース名: 指定したデバイスの詳細情報を表示
    - device connect インターフェース名: 指定したデバイスを接続
    - device disconnect インターフェース名: 指定したデバイスを切断
    - device modify
    - device monitor インターフェース名: 指定したデバイスを監視
    - device delete インターフェース名: 指定したデバイスを削除
    - device wifi list: WiFiアクセスポイントの表示
    - device wifi connect SSID: WiFiに接続するデバイスを作成、有効化
    - device wifi rescan: WiFiアクセスポイントの再検索


## Q
* ip コマンドのオブジェクト
    - IPアドレス
    - ネットワークデバイス
    - IPv4のARPキャッシュ、IPv6のNDキャッシュ
    - ルーティングテーブル
* そのオブジェクトに対するコマンド
.  
.  
.  
.  

## A
* ipコマンドのオブジェクト
    - addr
    - link
    - neighbour
    - route
* そのオブジェクトに対するコマンド
    - add, ad, a
    - del, de, d
    - show, sh, s

# セキュリティ

## Q
* find の -perm オプション
    - `-perm mode`
    - `-perm -mode`
    - `-perm /mode`
    - `-perm +mode`

.  
.  
.  
.  

## A
* find の -perm オプション
    - `-perm mode` mode (8進数表現でもシンボルでもよい) に完全に一致する。全てのビットを8進数かシンボルで表現しなければならない。
    - `-perm -mode` mode で指定した全て。例えば、-perm /222 は 222 のファイルにしかマッチせず、777 のファイルにはマッチしない。
    - `-perm /mode` mode で指定したいずれか。例えば、-perm /222 は 777 のファイルにもマッチする。
    - `-perm +mode` mode で指定したいずれか。現在は / の使用を推奨。


## Q
* fuser のオプション
    - あるファイルを使っているプロセスを特定する
    - あるTCPポートで通信しているプロセスを特定する
    - あるUDPポートで通信しているプロセスを特定する
    - 見つかったプロセスにSIGKILLを送信する
.  
.  
.  
.  

## A
* fuser のオプション
    - -n file ファイルパス
    - -n tcp ポート番号
    - -n udp ポート番号
    - -k

## Q
* xinetd の設定ファイル
* xinetd の設定項目
.  
.  
.  
.  

## A
* `/etc/xinetd.conf`
* 設定項目
    - bind, interface: サービスを提供するインターフェースのIPアドレス
    - disable yes|no: サービスの有効無効
    - instances: サーバープログラムの最大起動プロセス数
    - log_type: 記録するログファイルの絶対パスまたはsyslogサーバー
    - socket_type: サービスの接続タイプ（stream, datagram...) を指定
    - no_access: サービスへのアクセスを拒否する接続元
    - only_from: サービスへのアクセスを許可する接続元
    - server: サーバープログラムの絶対パス
    - server_args: サーバープログラムを起動するときの引数
    - user: サーバープログラムを起動するユーザー
    - wait yes|no: マルチスレッドならno


## Q
.  
.  
.  
.  

## A




* 白本 102 4章 システムサービスの管理
    - 時刻
        - システムクロック(Linux カーネル)、ハードウェアクロック(マザーボード)
            - 例えば date コマンドは、システムクロックに基づき、/etc/localtime を参照してローカルタイムに変換する
            - ハードウェアクロックのインターバルタイマー割り込みによってシステムクロックが進む
			- `hwclock -r` ハードウェアクロックを表示
            - 一方をもう一方に合わせることができる `hwclock -systohc` (system to hardware clock), `hwclock -hctosys` (hardware clock to system)
				- to hardWare `-w`, to Sys `-s`
        - NTP
            - NTPクライアントがNTPサーバーから得た時刻をシステムクロックに設定できる
            - NTPサーバーには stratum0, 1, 2... という階層がある。stratum 0 はリファレンスクロックと呼ばれ、原子時計やGPSといった厳密な時刻源である。これに基づいたNTPサーバーが stratum 1 である。最下位はstratum 16である。
            - /etc/ntp.conf NTPデーモンが参照するファイル
                - driftfile: NTPサーバーの参照時刻からのずれを記録するファイルを指定。/var/lib/ntp/drift
                - restrict: アクセスコントロールリストの指定
                - server: 外部NTPサーバーの指定。IPアドレスまたはDNS名(例: 0.rhel.pool.ntp.org)。ローカルのシステムクロックを指定する場合は server 127.127.1.0 と書く。
                    - デフォルトは64秒でポーリングする。指定したサーバーの後に iburst オプションをつけると2秒間隔になる。
			- ntpq: NTPサーバーとの同期状態を表示
				- -p 一覧表示
				- -t 対話モード
				- `*` 時刻同期中のNTPサーバー、`+` 時刻同期可能なNTPサーバー、`-` 参照しないNTPサーバー
				- 表示例と解説 http://www.usupi.org/sysad/215.html
			- ntpdate: NTPサーバーから現在時刻を取得してシステムクロックに反映させる
				- `ntpdate pool.ntp.org`
        - Chrony
            - NTPサーバー。ntpd の後継。chronyd がデーモン。chronyc が管理コマンド。
            - /etc/chrony/chrony.conf(Debian), /etc/chrony.conf(RedHat)
                - server ホスト名 (ntp.conf と同じく iburst が使える)
                - driftfile /var/lib/chrony/drift
				- rtcsync (システムクロックをハードウェアクロックに同期する。デフォルトでは11分ごとに。)
            - chronyd を有効化 `systemctl enable chronyd.service`
            - chronyc
                - 何もつけなければ対話モード(chronyc>)。オプションをつけることもできる。
                - `chronyc sources` 時刻源の情報を表示
				- `chronyc sourcestats` 時刻源の統計情報を表示
				- `chronyc tracking` 時刻同期の詳細情報を表示
        - timedatectl
            - systemd を利用して、日時、時刻、タイムゾーンを管理
            - `timedatectl list-timezones | grep Tokyo` Asia/Tokyo というタイムゾーンがあることがわかる `timedatectl set-timezone Asia/Tokyo`
            - `timedatectl set-time 'yyyy-mm-dd hh:mm:ss'` で手動設定できる
				- chronyd が動いていると設定できない `Failed to set time: NTP unit is active`
				- システムクロックとハードウェアクロックの両方が設定される
				- date の場合、書式が MMDDhhmmYYYY.ss である。
			- `timedate ctl set-ntp yes` NTPによる時刻同期有効無効設定
    - 時刻に基づいた実行
        - systemd の timer ユニット
            - 定期実行, 従来は cron
                - /etc/systemd/system/*.timer
                - .timer が .service を起動する
                - .service
                    - `RefuseManualStart=no` 間接起動のみ (systemd start *.service できない) `RefuseManualStop=yes` 手動停止は可能
                    - `ExecStart=実行したいコマンドのフルパス`
                - .timer
                    - `OnBootSec=1min` 起動後に実行する時間, `OnUnitActiveSec=3min` 実行間隔, `Unit=foo.service` 定期実行させたい処理
                    - .timer を書いたら有効化して `systemctl enable foo.timer` すぐ実行させたければ `systemctl start foo.timer`
                    - 作ったtimerが動いているか確認 `systemctl status foo.timer` timer群の中にあるか確認 `systemctl list-timers` 実行結果のログを確認 `journalctl -u foo`
            - 指定時間後に1回だけ実行 `systemd-run --unit=foo --on-active=60m 実行したいコマンド`
        - cron
            - 設定変更 `crontab -e` デフォルトでviが起動する。環境変数VISUALまたはEDITORで変えられる。
            - 設定すると `/var/spool/cron/ユーザ名` が設定ファイルとして保存される
            - システムのcrontab設定は `/etc/crontab`
            - ユーザーがcronを使えるか `/etc/cron.allow`(ホワイトリスト), `/etc/cron.deny`(ブラックリスト) で設定できる。
            - 今の設定確認 `crontab -l`
    - システムログ
        - 古い方より4方式 syslog, rsyslog, syslog-ng, systemd journal (syslog-ng だけ後方互換性がない)
		- https://access.redhat.com/documentation/ja-jp/red_hat_enterprise_linux/7/html/system_administrators_guide/ch-viewing_and_managing_log_files
        - systemd journal
            - カーネルのログ /dev/kmsg, サービスのログ stdout/stderr, アプリケーションのsyslog()経由によるログ /dev/log を扱う
            - 揮発ログ /run/log/journal/マシンID/*.journal (バイナリファイル)
            - 不揮発ログ /var/log/journal/マシンID/*.journal (バイナリファイル)
            - systemd-journal を採用している多くのディストリビューションでは rsyslog と組み合わせている
                - /run/systemd/journal/syslog (ソケットファイル)を rsyslogd が読み、/dev/console, /var/log/messeges, /var/log/secure を出力
            - /etc/systemd/journald.conf
                - デフォルトでは再起動するたびにログが消える Storage=persistent によって永続化（いらんと思うけど）
            - `systemd-cat コマンド` コマンドの実行ログが journald で扱う
            - journalctl コマンド
				- 全て表示 -a, --all
                - 時間範囲内のログ --since="" --until=""
                - 指定プライオリティ以上 -p, --priority
                - リアルタイムに表示 -f, --follow
                - 最新のものを表示(古い順に表示して最後に飛ぶ) -e, --pager-end
                - 新しい順に表示 -r, --reverse
				- 特定プロセスのログを表示 _PID=
				- 特定ユーザーのログを表示 _UID=
        - syslog, rsyslog
            - /etc/syslog.conf
            - 指定したプライオリティ以上のログを記録する `ファシリティ.プライオリティ ログ出力パス` (例: mail.info /var/log/maillog)
            - 指定したプライオリティのみのログを記録する場合は `ファシリティ.=プライオリティ ログ出力パス` (例: kern.=crit /var/log/messages) こんなことしないけど
            - ファシリティ: kern カーネル(0), user(1), mail(2) ... ftp(11) まで予約されていて、local0 (16) ～ local7 (23)がローカル用。
            - プライオリティ: 最高から emerg, alert, crit, err, warning, notice, info, debug, none(記録しない).
                - よく見る /var/log/messages には、だいたいのファシリティのinfo以上のメッセージが記録される。（例外: mail, news, authpriv)
			- ログ出力パスの代わりに外部の syslog サーバーを指定可能 `@サーバーホスト名`
            - logger
                - 任意のファシリティとプライオリティのログをsyslogに送る。例: `logger -p user.info "Syslog Test"` を実行すると /var/log/messages に記録される
			- https://www.infraeye.com/study/linuxz45.html
* 白本 102 5章 ネットワークの基礎
    - IPv4
        - ホスト部で使えるビット数から使えるアドレス数を計算、ネットワークアドレス、ブロードキャストアドレス、ルーターの3つを引いたものがホストとして使えるアドレス数
            - /26 の場合、2^6 - 3=61
        - あるIPアドレスがローカルネットワークに存在するかの判断は、そのアドレスにネットマスクを被せた結果がローカルホストのネットワークアドレスに一致するかで判断
    - IPv6
        - 128ビット、フルで書くと:が7つ 0000:ffff:0000:ffff:0000:ffff:0000:ffff, 0 が連続するフィールドを1箇所だけ :: と省略できる, ブロードキャストがなくマルチキャストを使う
        - Global Unicast Address: 全IPv6ネットワーク, 2001::, 2002::, 2003::
        - Unique Local Address: 組織内ネットワーク, fc00::
        - Link Local Address: 組織内ネットワークの1セグメント, fe00::
    - /etc/services
        - サービスとポートの対応。ftp(20), ssh(22), smtp(25), domain(53), http(80), https(443) など。domain は DNS を表すことに注意(dns と書かれない)。
    - 0-1024 特権が必要なポート。一般ユーザーはバインドできない。
    - xinetd
        - ネットワークからのサービスリクエストを受け付け、リクエストに対応したサーバプロセスを起動するデーモン
    - netstat
        - TCP, UDP のサービスポート状態(-t, -u), UNIXドメインソケットの状態(-x), ルーティング情報(-r)。TCP,UDP,UNIX全部入り(-a, --all)。`netstat --ar`
        - IPアドレスはドメイン名で、ポート番号はサービス名で表示される。-n (numeric) をつけると数字で表示される。
        - -nr において Destination が 0.0.0.0 のエントリがデフォルトルート 
        - 何のプロセスがポートを開いているか -p で確認可能
        - 何をLISTENしているかで何のサーバーか推測可能（例：smtp を LISTEN している→メール送信サーバー）
    - ping6
        - IPv6 アドレスに対する ping コマンド。リンクローカルアドレスを指定する場合は `ping6 -I eth0 fe80::........` のようにネットワークインターフェースを指定する
    - traceroute, traceroute6
        - デフォルトは UDP。-I で ICMP。
    - ip
        - ネットワークインターフェースの表示と設定、ルーティングテーブルの表示やエントリの追加と削除。ifconfig, route, netstat の後継にあたる。
        - link
            - eth0 を有効化 `ip link set eth0 up`
                - ifconfig なら `ifconfig eth0 172.16.0.1 up`
            - eth0 の通信量を表示 `ip -s link show eth0`
        - addr
            - eth0 のネットワークアドレス設定 `ip addr add 172.16.0.2/16 dev eth0`
        - route
            - ルーティングテーブルの表示 `ip route`
            - ルーティングテーブルにエントリを追加 `ip route add 172.16.0.2/16 via 172.16.255.254`
    - nmcli
        - device
            - 何のネットワークインターフェース（eth0 など）があるか `nmcli device`
        - general
            - このマシンのホスト名を表示 `nmcli general hostname`
            - このマシンのホスト名を設定 `nmcli general hostname NEW_HOST_NAME`
        - connection
            - 接続名、接続UUID、接続タイプ、デバイスを表示（例：有線LANポート、WiFi の情報を表示）`nmcli connection`
        - networking
            - インターネットにどこまで接続できているか `nmcli networking connectivity` {none, portal, limited, full} Windows のタスクバーでたまに出る制限付きみたいなものだと思う
* セキュリティ
	- ssh
		- 公開鍵認証
			- ホスト認証（クライアントがサーバーの公開鍵を未入手）：ユーザーがサーバーの公開鍵（のフィンガープリント）に対してyesと入力すればknown_hostsにサーバーの公開鍵が保存される。
			- ホスト認証（クライアントがサーバーの公開鍵を入手)：サーバーがクライアントにサーバーの公開鍵を送る。クライアントはknown_hostsにある公開鍵と比べる。比較結果が一致した場合（または初回の接続でサーバーの公開鍵を入手した場合）、クライアントはサーバーの公開鍵を用いて暗号化したデータを作成し、サーバーに送信する。サーバーはそのデータをサーバーの秘密鍵（サーバーにしかない）で複合し、複合データをクライアントに返す。クライアントは、返されたデータと送ったデータが一致すれば正しいサーバーホストと判断する。
			- ユーザー認証：ユーザーは自身の公開鍵をサーバーに事前に登録しておく。ユーザーは自身の秘密鍵で電子署名を生成する。サーバーはその電子署名をユーザーの公開鍵で検証する。
	- gpg
		- -e, --encrypt
		- -k, --list-keys, --list-public-keys
		- -r, --recipient
		- --sign
		- --verify