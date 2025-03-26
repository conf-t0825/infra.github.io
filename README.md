＃eBGPの冗長化とAnsibleを使ってshowコマンド取得の練習

#実施したい内容については、次に記載の通りである。
・R1とR2間、R5とR6間は、EIGRP1002でダイナミックルーティングさせる。
・R1でloopbackを使用して、各セグメントを持たせる。
・R2でEIGRP1002からBGP65001に再配送させ、再配送させる際にBGPのAS Path属性を持たせて重み付けさせルートマップを使用して通信を制御させ通常時は、プライマリールートを使ってリモートASへ通信させる様にする。
またリモートAS障害が発生した際は、セカンダリールートを使ってリモートASへ通信出来るように冗長化させる。
・R2とR5は、ASの異なるeBGPで構築する。
・eBGP間のIGPは、EIGRPを使用する。通常時のプライマリールートは、EIGRP1000を使用し、障害時のセカンダリールートはEIGRP1001を使用する。
・セグメントやポートの情報については、構成図の通り。
・ルーターの設定が終わり次第、ping及びtracerouteを使用して正しく想定通りの疎通が出来るか確認を行う。
・ping及びtracerouteが問題ない事を確認出来次第、Ansibleを使ってshowコマンドを取得できるようにインベントリーファイルとplaybookを作成する。
・playbook実行後想定通りであるか、エラーが発生していないかログの確認を行う。

#Ansibleを使って取得するshowコマンドの一覧
・show version 
・show interfaces 
・show interfaces counters errors
・show ip route vrf *
・show ip interface brief
・show cdp nei
・show logging
・show ip eigrp nei
・show ip eigrp top all
・show ip bgp nei
・show ip bgp neighbors advertised-routes
・show ip bgp neighbors received-routes
・show ip bgp all
・show ip bgp route-map AS-path
・show running-config
