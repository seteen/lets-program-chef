Chefのセットアップ
===
## インストール
1. rubyのインストール  
省略します
2. chefのインストール  
```
gem install chef --no-ri --no-rdoc # chefの本体
```
3. knife-soloのインストール
```
gem install knife-solo --no-ri --no-rdoc # chef(knife)のプラグイン
```
4. berkshelfのインストール
```
gem install berkshelf --no-ri --no-rdoc # サードパーティのクックブックを管理しやすくするgem
```

## 初期設定
Chefの初期設定を行う
```
knife configure # knifeはchefのインストールで一緒に入るコマンド。色々聞かれるが全てEnterで良い
```

## ディレクトリの作成
```
knife-solo init chef-directory

## 下記のようなフォルダができるはず
$ tree chef-directory/
chef-directory/
├── cookbooks
├── data_bags
├── environments
├── nodes
├── roles
└── site-cookbooks
```

## 自分のクックブックの作成
上で作成したディレクトリにて下記を実行
```
knife cookbook create <COOKBOOK NAME> -o site-cookbooks/
```

## サードパーティ製のクックブックを利用する
サードパーティ製のクックブックは[ここ](https://supermarket.chef.io/cookbooks)で探しましょう  
Berkshelfを利用します。ディレクトリのルートにBerksfileを作成する
```
vim Berksfile
```
Berksfileは下記のようになります
```
site :opscode
cookbook 'yum' # 探してきたクックブックを貼る（バージョン指定は cookbook 'yum', '~> 3.8.2'のようにやる）
cookbook 'mysql'
```
次のコマンドでサードパーティのクックブックがcookbooksディレクトリに入ります
```
berks install
```
