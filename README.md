# nginx + php-fpm + mysql

```
+-----------+      +-----------+      +---------+ 
| webserver | <--> |    app    | <--> |   db    | 
|  (nginx)  |      | (php-fpm) |      | (mysql) | 
+-----------+      +-----------+      +---------+ 
```
※ webserver <---> app のやり取りはUNIXドメインソケットを使用

## 構造
```
❯ tree
.
├── README.md
├── compose.yaml                       # docker compose のためのファイル
├── docker                             # docker: コンテナイメージを作成するために必要ファイルを配置
│   ├── nginx                          # nginx: nginxイメージのためのファイルを配置
│   │   ├── Dockerfile
│   │   └── conf
│   │       ├── conf.d
│   │       │   ├── default.conf
│   │       │   └── upstream.conf
│   │       └── nginx.conf
│   └── php-fpm                        # php-fpm: php-fpmイメージのためのファイルを配置
│       ├── Dockerfile
│       └── conf
│           └── php-fpm.d
│               └── zz-docker.conf
└── src                                # src: ソースコードを配置
    ├── app                            # app: エントリーポイントのphpから読み込まれるphpを配置
    │   ├── app.php
    │   └── template
    │       └── index.tpl.php
    └── public                         # public: ドキュメントルートにするディレクトリ
        └── index.php                  # エントリーポイントになるphp

12 directories, 11 files
```

