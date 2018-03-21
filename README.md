# raspberrypi_first_setup  
raspberrypi の初期設定を ansible で実行できるようにまとめたものです  
初期設定される内容は以下のとおりです  

- timezone の設定
- ホスト名の設定
- /etc/hosts のホスト名の設定
- apt-get -y update の実行
- apt-get -y upgrade の実行
- apt-get -y dist-upgrade の実行
- IP アドレスの変更
- サーバ再起動


## Requirements  
以下の環境で実行確認はしています  

- ansible 2.4.3+
- Python 2.7+

## Usage
* 対象の raspberrypi に ssh 鍵認証でログインできる状態であることを確認します  
```bash
ssh 'raspberrypi 名'
```

* 使用する環境に合わせてファイルの記述を修正します
** hosts/production ファイルの修正
```bash
vi hosts/production
---
raspberrypi 名に変更します
```

** host_vars/rasp1
```bash
vi host_vars/rasp1
---
my_ipaddr: "設定するIPアドレス"
my_gateway: "設定するゲートウェイ"
my_dns: "設定するDNSサーバ"
```

```bash
mv host_vars/rasp1 host_vars/hoge <- raspberrypi 名に変更します
```

* エラーが発生しないかテストします
```bash
ansible-playbook site.yml --check -D
```

* 実行します
```bash
ansible-playbook site.yml
```

* 再起動がされるため、/etc/hosts や ~/.ssh/config に新しいホスト名とIPアドレスの記述をしてssh などで疎通確認を実施します





