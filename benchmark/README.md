# Groongaとの比較のベンチマーク取得手順

## 前提

 * node0, node1, node2の3台のコンピュータがあると仮定し、これらをDroongaクラスタにする。
 * 比較用としてGroongaをnode0にインストールする。
 * ベンチマークのクライアントは、node3で実行する。

ネットワーク構成と各マシンの役割は以下の通り。

    (internet)
       |
    [192.168.10.0/24]
       |
       +-[node0: 192.168.10.50] droonga-1
       |
       +-[node1: 192.168.10.51] droonga-2
       |
       +-[node2: 192.168.10.52] droonga-3
       |
       +-[node3: 192.168.10.53] benchmark client

 * node0
   * OS: Ubuntu 14.04LTS
   * CPU: Intel Core i5 M460 2.53GHz
   * Memory: 8GB
 * node1
   * OS: Ubuntu 14.04LTS
   * CPU: Intel Core i5 650 3.20GHz
   * Memory: 6GB
 * node2
   * OS: Ubuntu 14.04LTS
   * CPU: Intel Core i5 650 3.20GHz
   * Memory: 8GB
 * node3
   * OS: Ubuntu 14.04LTS
   * CPU: Intel Core i5-4300U vPro 1.90GHz
   * Memory: 8GB

## 手順

基本的な手順は[Droongaチュートリアル：DroongaとGroongaのベンチマークの取り方](http://droonga.org/ja/tutorial/1.0.8/benchmark/)に則る。

### データベースサイズ

上記の検証環境では、ノードのうち2台が8GB、1台が6GBのメモリを積んでいる。
なので、純粋な性能比較のためのベンチマークとしては、最大で6GB程度のデータベースサイズに留める必要がある。

今回は150万件のページを各ページごとに最大1000文字まで変換したデータに基づく4.3GiBのデータベースでベンチマークを行った。

