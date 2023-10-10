# Robust-Ruby-on-Rails


# About Ruby on Rails
[公式サイト](https://rubyonrails.org/)  
勝手な所感...  
Djangoと同じでルールを守る系のフレームワーク  
どのディレクトリに存在するか?、命名が統一されているか?などで記述を減らす思想なので、最初はなれるまで大変そう  


**大事なポイント**
- お作法をしっかり知る
- しっかり公式ドキュメントを読んで裏側の構造を理解する


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


## お作法
### 1. ルーティングとオートローディング
`ApplicationController`を継承したControllerクラスを参照している  
超詳しくは、[こちら](https://guides.rubyonrails.org/autoloading_and_reloading_constants.html)  
※ [zeitwerk](https://github.com/fxn/zeitwerk)によって、requiredなしにimportできる(名称から解析されるので、基本的に命名は従う方が吉)

```ruby
Rails.application.routes.draw do
  # どのControllerをルートに設定するか?
  root "articles#index" # `app/controllers/articles_controller#index`が呼ばれる

  # 具体的なルーティング設定
  get "/articles", to: "articles#index" # Getの場合、`app/controllers/articles_controller#index`が呼び出される
  get "/articles/:id", to: "articles#show"
end
```

#### リソースフルなルーティング
`articles`のModel, View, Controllerを組み合わせる場合、そのエンティティ(Article)をリソースと呼ぶ
リソース指定でもいける  
```ruby
Rails.application.routes.draw do
  root "articles#index"

  resources :articles
end
```


### 2.　Model
データを表すためのクラス  
`ActiveRecord`クラスを継承することで、Railsの機能を通じてアプリケーションとデータベースを連携する機能が提供される  

Railsにはモデルジェネレータが存在し、雛形を作成してくれる  
```shell
bin/rails generate model Article title:string body:text
```
migrationについても提供されている
```shell
bin/rails db:migrate
```
### モデルの操作
[ActiveRecordの基本](https://guides.rubyonrails.org/active_record_basics.html)
```ruby
Article.all
Article.find(id)
article = Article.new(title: "...", body: "...")
article.save
...
```

### 3. Controller
`ApplicationController`を継承する  

```ruby
class ArticlesController < ApplicationController
  def index
    @articles = Article.all
  end
end
```

### 4. View
コントローラーのインスタンス変数(`@変数`)には、Viewからアクセスできる  
`<% %>`はRubyコードの評価  
`<%= %>`はコードを評価し、戻り値を返す  
```html
<ul>
  <% @articles.each do |article| %>
    <li>
      <%= article.title %>
    </li>
  <% end %>
</ul>
```