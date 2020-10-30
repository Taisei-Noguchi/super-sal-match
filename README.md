# README

# アプリケーション名
SalMatch（サルマッチ）

# 概要
フットサルのメンバーや対戦チームの募集ができます。他にも環境やレベルを選択して募集内容を見ることもできます。

# URL
https://super-sal-match.herokuapp.com/

# テスト用アカウント
投稿者
ニックネーム：イチロー
アドレス：aaa@icloud.com
パスワード:11111111

閲覧者
ニックネーム：ジロー
アドレス：bbb@icloud.com
パスワード：22222222

# 利用方法
ログインしなくてもトップページと詳細ページを閲覧することは可能です。

ユーザー登録機能：ブラウザ右上にある新規登録ボタンまたはログインボタンを押す。フォームに沿ってユーザー情報を入力する。入力が完了したらブラウザ下部の登録ボタンを押す。
投稿機能：ブラウザ右上にある投稿ボタンを押して、フォームに沿って投稿内容を入力する。入力が完了したらブラウザ下部の登録ボタンを押す。
コメント機能：ログインした状態で、詳細ページのコメントフォームにコメントを入力して、送信ボタンを押す。

# 制作背景
フットサルやサッカーを楽しむには専用のシューズが必要です。シューズは環境に応じて種類が異なります。例えば天然芝と人工芝ではシューズの裏側についているポイントが異なり、人工芝で天然芝ようのシューズを使用すると人工芝が痛んでしまいます。そのため、フットサルをするには環境ごとに対応しているシューズが必要となり、持っているシューズが対応している環境でないとプレーできません。私もフットサルをやっていて、フットサルのマッチングアプリを使って試合に参加しようとしたことがあります。アプリの情報を頼りに準備をして会場に着くと、アプリを見る限りでは、天然芝であると思っていたのに、実際は人工芝で人工芝用のシューズがなく参加できないことがありました。フットサルのマッチングアプリには会場名は記載されていても、フィールドの環境までは記載されておりません。そこでフィールドの環境がわかりやすく明記されていれば、この問題を解決できるのではないかと考え、このアプリを作成しました。

# 洗い出し要件
AWS
目的：AWSのS3に画像を保存するため。
詳細：画像の保存はAWS S3で行うことで、デプロイや再起動しても画像がリンク切れにならないようにすることができる。
ストーリー：表示されている画像がAWS保存されている。
見積もり:12時間

コメント機能
目的：コメントでユーザー同士がコミュニケーションが取れるようにするため。
詳細：詳細ページからコメントを書くことができる。
ストーリー：詳細ページからコメントを書くことができる。
見積もり:12時間

ユーザー管理機能
目的：ユーザー管理を行うため。
詳細：新規登録、ログイン、ログアウトができる。
ストーリー：トップページ右上にある新規登録ボタンやログインボタンから、アプリにログインできる。
見積もり:12時間

投稿機能
目的：募集ページを投稿するため。
詳細：募集ページを投稿できる。
ストーリー：ログインすることで、トップページ右上に投稿ボタンが出現し、フォームを入力して投稿ボタンを押すことで、投稿できる。
見積もり:12時間

# テーブル設計
usersテーブル

| Column     | Type    | Options      |
| ---------- | ------- | ------------ |
| nickname   | string  | null: false  |
| email      | string  | null: false  |
| password   | string  | null: false  |

Association

- has_many :tweets
- has_many :comments

tweetsテーブル

| Column          | Type        | Options                       |
| --------------- | ----------- | ----------------------------- |
| title           | string      | null: false                   |
| place           | string      | null: false                   |
| address         | string      | null: false                   |
| price           | string      | null: false                   |
| item            | string      | null: false                   |
| category_id     | integer     | null: false                   |
| field_id        | integer     | null: false                   |
| level_id        | integer     | null: false                   |
| month_id        | integer     | null: false                   |
| day_id          | integer     | null: false                   |
| hour_id         | integer     | null: false                   |
| user            | references  | null: false, foreign_key:true |

Association

- has_many :comments
- belongs_to :user

commentsテーブル

| Column          | Type        | Options                       |
| --------------- | ----------- | ----------------------------- |
| text            | text        | null: false                   |
| user            | references  | null: false, foreign_key:true |
| tweet           | references  | null: false, foreign_key:true |

Association

- belongs_to :user
- belongs_to :tweet

# ローカルでの動作方法
ターミナルに以下のコードを上から順に入力する。
cd projects
git clone https://github.com/Taisei-Noguchi/super-sal-match.git
cd super-sal-match
bundle install
yarn install
rails db:create
rails db:migrate