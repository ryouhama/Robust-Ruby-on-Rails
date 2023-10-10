# Robust-Ruby-on-Rails
Ruby on Rails Guides

# About Ruby on Rails
[公式サイト](https://rubyonrails.org/)

## Ruby on Railsの思想
- Don't Repeat Yourself(繰り返しをしない)  
  DRY はソフトウェア開発の原則で、「すべての知識は、システム内で単一の、明確で権威のある表現を持たなければならない」と述べています。  
  同じ情報を何度も書かないことで、コードの保守性、拡張性が向上し、バグが少なくなります。

- Convention Over Configuration(設定よりも規約を)  
  Rails には、Web アプリケーションで多くのことを実行するための最良の方法についての意見があり、  
  無限の設定ファイルを通じて細部を指定することを要求するのではなく、この一連の規約をデフォルトとしています。

## Getting Started
### Install `rails`
```shell
gem install rails
```

### Creating the Application
```shell
rails new [your_applicaiton_name]
```

### Starting Up the Web Server
```shell
# Your application name is `blog`.
blog/bin/rails server
```

### DB Migration
コマンドでテーブルのテンプレートつくってくれる
```shell
# テーブル: Article
# カラム: title, body, created_at, updated_at
bin/rails generate model Article title:string body:text
```
`db/migrate`にタイムスタンプ付きのmigrationファイルを作成する
```shell
bin/rails db:migrate
```

### Rails Console
DjangoのShell_plusみたいなもん
```shell
bin/rails console
```
