samba_vpn
=========

外出中に、Mac OS Xで家のファイルサーバの中を見たい時があると思います。  
直接は怖いのでVPN越しにファイルサーバを運用している場合、VPNのパネルから「接続」ボタンを押し、さらにFinderを開いて「サーバへ接続」を押し、ファイルサーバのIPアドレスを入力し（例えばsmb://192.168.1.3）接続、としていました。  
GUIを触るのが恐ろしく面倒だったのでコマンドラインからできるように作成しました。

一度設定してstartすれば自動的にVPNを張ってSambaでマウントしてくれます。

## 使い方
### VPNの設定
「システム環境設定」→「ネットワーク」からVPNの設定をしておいて下さい。  
ググれば出るのでお任せします。  
今回は「test_vpn」という名前で作成したとします。

### スクリプトを落とす
適当なディレクトリに移動してからスクリプトを落として下さい。  
今回は~/Documentsとします。

    $ cd ~/Documents
    $ git clone https://github.com/knqyf263/samba_vpn.git
    $ cd samba_vpn
  
### 設定ファイルを書き換える
まずvpn.conf.sampleがあるので、それをvpn.confに直し、その中身を書き換えます。
 
    $ cp vpn.conf.sample vpn.conf

ファイルサーバのアドレスが「192.168.1.3」で、ユーザ名が「user」、パスワードが「password」、マウントしたいディレクトリが「test_dir]の場合以下のようになります。

    $ vim vpn.conf
    
    # VPN name
    VPN="test_vpn"
    # IP address of file server 
    SMB="192.168.1.3"
    # User for file server
    USER="user"
    # If you need
    PASSWORD="password"
    # directory which you want to mount
    DIR="test_dir"
    
ゲストユーザーの場合、ユーザ名を「guest」、パスワードを空にすれば繋がります。 

## 実行
startしたい場合はstartを渡し、止めたい場合はstopを渡します。
    
    $ chmod a+x mount.sh
    $ ./mount.sh start
    
