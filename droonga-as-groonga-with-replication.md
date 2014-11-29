# Droonga

subtitle
:   　　
    分散Groongaで
    快適レプリケーション生活

author
:   結城洋志

institution
:   株式会社クリアコード

allotted_time
:   30m

theme
:   groonga

# Droongaって？

*D*istributed G*roonga*

# 要旨

 * 1年間の*進捗報告*
 * *「分散Groonga」としての
   Droongaの現状*の紹介

# 今日話すこと

 * 分散型データ処理エンジン
   *Droonga*の
 * 組み込みプラグインの1つ
   *Groongaプラグイン*
   * 使い方
 * Groonga v.s. Droonga

# 今日話さないこと

 * Droongaの*設計*のこと


# Part1

-Part1-
1年間の
*進捗報告*

# 昨年の発表

 * 設計方針
 * 実装
 * （当時の）現状
 * （当時の）今後の予定

# 大まかに言って

 * *全く新しい・汎用の*分散型
   データ処理エンジンとして
   * 「こういう*設計*でこう動きます」
   * 「こういう事も
     *やろうと思えばできます*」
 * 「こうやって*今すぐ試せます*」
   という話はあまり無かった

# なんで？

 * どっちかというと*フレームワーク*
 * *具体的な用途*を先に
   決めないと話が始まらない
 * 全文検索をやりたいだけでも
   やり方が*Groongaとは全く違う*

# ハードル高すぎ

![](images/parts.jpg){:relative_height="95"}

# 使うとしても

 * 設計を*熟知*した人が
 * 用途ごとの*最適な構成*を考え
   * ログ保存＆検索用？
   * 掲示板のバックエンド用？
 * 丁寧な*手作業*でひとつひとつ
   セットアップ＆設定

# 職人芸の世界

![](images/syokunin.jpg){:relative_height="95"}

# 問題

 * ユーザにとって
   * *気軽*に試せない
   * *Groongaユーザ*には馴染みにくい
 * 開発者にとって
   * 「汎用かつ便利」は作るのが大変
   * *Groongaユーザ*を長く放置してしまう

# 当初の開発方針

![](images/development-policy-before.png){:relative_height="95"}

# 進め方を見直し

![](images/development-policy-after.png){:relative_height="95"}

# どう変わった？

 * 変わらないこと
   * 最終的に作る*物*
 * 変わったこと
   * 作る*順番*
   * プロジェクト外への*見せ方*

# ここまでの成果(1)

 * *Groongaとの互換性*向上
 * *簡単インストール＆
   セットアップ*
 * 管理コマンドによる
   *簡単クラスタ管理*

# すぐ使える

    $ curl "http://...engine.../install.sh" | \
             sudo bash
    $ curl "http://...http-server.../install.sh" | \
             sudo bash
    $ service droonga-engine start
    $ service droonga-http-server start

    $ droonga-engine-join --host=node1 \
                          --replica-soruce-host=node0
    $ droonga-engine-join --host=node2 \
                          --replica-soruce-host=node0

    $ curl "http://hostname:10041/d/select?..."

# ここまでの成果(2)

 * *オーケストレーション*
   （based on Serf）
   * 一部のノードが死んでも
     クラスタとして動作し続ける
 * *チュートリアル*の充実

# 結果

*レプリケーションできるGroonga*

としてそこそこ
使えるようになってきたはず



# Part2

-Part2-
*分散Groonga*
としての
Droongaの紹介

# 特徴

特徴

# Groonga互換

![](images/groonga-vs-droonga-compatible-http.png){:relative_height='95'}

# データベースを分散

 * *レプリケーション*
   * 現在の開発はここに注力
 * *パーティショニング*
   * 現在は部分的に対応（これから改善）

# レプリケーション

![](images/replication-write.png){:relative_width="35" align="left" relative_margin_left="-20"}

![](images/replication-read.png){:relative_width="45" align="right"}

システムの冗長性や
耐障害性が高まる

# パーティショニング

![](images/partition-write.png){:relative_width="40" align="left" relative_margin_left="-20"}

![](images/partition-read.png){:relative_width="50" align="right"}

より多くの量のデータを管理できる


# 実際の性能は？

Groonga v.s. Droonga
ベンチマーク

 * Wikipedia日本語版
   *150万ページ*
 * *全文検索*＋*ドリルダウン*
 * キャッシュヒット率50％
 * [詳細はリポジトリを参照](https://github.com/droonga/presentation-groonga-night-5-droonga-as-groonga-with-replication/tree/master/benchmark)

# スループットの比較

![](images/throughput.png){:relative_height='95'}

# レイテンシーの比較

![](images/latency.png){:relative_height='95'}

# 性能の傾向

 * *スループット性能*は良好
 * *レイテンシー*は若干ある
   * 同時接続数が多いと性能が逆転
 * ノード追加で*Groongaの
   性能上の限界*を超えられる

# これからのDroonga

 * Groonga互換
   * *Suggest*（ローマ字前方一致検索）
 * 汎用分散データ処理エンジン
   * 完全*無停止*でのクラスタ構成変更
   * *パーティショニング*有りの構成
   * *プラグイン開発*をより容易に


# まとめ

まとめ

# まとめ

 * Droongaは*汎用の
   分散型データ処理エンジン*
 * 組み込みのプラグインによって
   *レプリケーション有りの
   Groonga*として使える

# 質問？

質問？


# Part3

-Part3-
Droongaを
*試してみよう*

# 試してみよう

 * インストールと起動
 * Groongaからのデータ移行
 * Groongaアプリケーションの
   バックエンドを
   Droongaに切り替え
 * クラスタにノードを追加

# ノードのセットアップ

インストールスクリプト
（Ubuntu、CentOS7のみ対応）

    # curl \
        https://raw.githubusercontent.com/droonga/droonga-engine/master/install.sh | \
        bash
    # curl \
        https://raw.githubusercontent.com/droonga/droonga-http-server/master/install.sh | \
        bash

# サービスの起動

serviceコマンドを使用

    # service droonga-engine start
    # service droonga-http-server start

# サービスの終了

serviceコマンドを使用

    # service droonga-engine stop
    # service droonga-http-server stop

# データの移行

    % sudo gem install rroonga grn2drn droonga-client

    % grndump --no-dump-tables /path/to/groonga/db | \
          grn2drn | \
          droonga-send --server=node0 \
                       --report-throughput)
    % grndump --no-dump-schema --no-dump-indexes \
              /path/to/groonga/db | \
          grn2drn | \
          droonga-send --server=node0 \
                       --server=node1 \
                       --server=node2 \
                       ...
                       --report-throughput)

# アプリケーションの移行

GroongaのHTTPインターフェースと
互換性あり

    curl "http://hostname:10041/d/select?..."

アプリケーションは接続先を
Droongaに変えるだけでOK

# クラスタへのノード追加

    % droonga-engine-join --host=cccc \
                          --replica-source-host=bbbb

![](images/join.png){:relative_height='100'}

# ノードの切り離し

    % droonga-engine-unjoin --host=cccc

![](images/unjoin.png){:relative_height='100'}




# 再度まとめ

 * Droongaは*汎用の
   分散型データ処理エンジン*
 * 組み込みのプラグインによって
   *レプリケーション有りの
   Groonga*として使える
 * HTTPインターフェースは
   *Groongaと互換性有り*



# 宣伝

宣伝

# 株式会社クリアコード

 * *Groonga有償サポート*
   * Groonga以外のGroonga族も
 * Mozilla有償サポート
   * Firefox, Thunderbird, Firefox OS
 * その他OSS開発全般
 * *コードリーダー育成支援*

# 個人の活動

*日経Linux*誌にて

シェルスクリプト
解説マンガ
*#!シス管系女子*
連載中

![](images/syskan.jpg){:relative_width="30" align="right" relative_margin_right="-10"}

# おわり

*Droonga, Groonga, 
株式会社クリアコード*
を宜しくお願いします

 * 使用画像
   * [写真素材 足成：秋葉原](http://www.ashinari.com/2009/07/12-024265.php)
   * [職人のおじいちゃん by Neil_Scottuk](http://free-photos.gatag.net/2014/07/06/100000.html)

