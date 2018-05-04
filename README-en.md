# el-training

## Introduction

This is the curriculum used by Everyleaf Corporation for internal training. All new employees, regardless of their skill level, are required to complete the entire course, which covers various topics considered basic knowledge for an Everyleaf Ruby on Rails developer. The training period is not fixed and ends when the trainee finishes all steps.

\* We plan to have mentors to estimate a reasonable training period in the future.

## License

This curriculum is licensed as [Attribution-NonCommercial-ShareAlike 4.0 International](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.ja).

[![クリエイティブ・コモンズ・ライセンス](https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png)](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.ja)  

## Outline

### System Requirements

This curriculum expects the trainee to build a task management system. It should include the following features:

- task creation
- due date for tasks
- priorty for tasks
- managable task statuses (todo, doing, done)
- filter tasks by status
- search tasks by title or description
- complete list of tasks, sortable by priorty and due date
- categorize tasks by adding labels
- logged in users can choose to see only tasks created by themselves

In addition, to complement the above requirments, the following features should also be implemented:

- user management

### Supported Browsers

- it should support the latest versions of macOS/Chrome

### Application (Server)

It should be built with the following language and middleware, with the latest stable version:

- Ruby
- Ruby on Rails
- PostgreSQL

Server side, it should use the following services:

- Heroku
- (optional) EC2 instance with AWS account
  - t2.micro（Amazon Linux）
  - RDS

\* We do not focus on performance and security here, but it should have reasonable quality. Extremely slow response times will be asked to improve.

## Final Goal

After completing this curriculim, we expect trainees to be able to:

- build a basic web application with Rails
- deploy a Rails applicaiton, with a common server setup
- add new features, perform data maintenance to a deployed Rails application
- send pull requests on GitHub (the entire flow), and learn the necessary Git commands
	- commit in appropriate sizes
	- write good commit messages
	- respond accordingly to code reviews
- ask questions (either verbal or by text) at the right time, to the right person (currently, their mentor)

## Assignment Steps

### Step 1: Rails development environment setup

#### 1-1: install Ruby

- install the latest version of Ruby with [rbenv](https://github.com/rbenv/rbenv)
- confirm the installed Ruby version with `ruby -v`

#### 1-2: install Rails

- install Rails with a gem command
- install the latest version of Rails
- confirm the installed Rails version with `rails -v`

#### 1-3: install database (PostgreSQL)

- install PostgreSQL, respective to your operating system
	- if using macOS, install with `brew`

### Step 2: create a GitHub repository

- install git
	- macOS: install with `brew`
	- add user name and email with `gitconfig`
- think about the application name (= repository name)
- create a repository
	- create a GitHub account if needed
	- create an empty repository

### Step 3: create a Rails project

- `rails new` コマンドでアプリケーションに最低限必要なディレクトリやファイルを作成しましょう
- `rails new` してできたプロジェクトのディレクトリ（アプリ名のディレクトリ）の直下に `docs` というディレクトリを作り、この文書ファイルをコミットしましょう
  - このアプリの仕様を管理下に置き、いつでも見られるようにするためです
- 作成したアプリをGitHub上に作成したリポジトリにpushしましょう
- バージョンを明示するため、利用するRubyのバージョンを `Gemfile` に記載しましょう（Railsは既にバージョンが記載されていることを確認しましょう）

### Step 4: visionize the application

- 設計を進める前に、どのようなアプリになるか完成イメージを（メンターと一緒に）考えてみましょう。ペーパープロトタイピングによる画面設計などがおすすめです
- システムの要件を読んで、必要なデータ構造を考えてみましょう
  - どのようなモデル（テーブル）が必要そうか
  - テーブル内にどのような情報が必要そうか
- データ構造を考えたら、それをモデル図に手書きで書いてみましょう
  - 完成したら撮影して、リポジトリに入れましょう
  - `README.md` にテーブルスキーマを記載しましょう（モデル名・カラム名・データ型）

※ 現時点で正解のモデル図を作成する必要はまだありません。現時点での想定として作ってみましょう（今後のステップで間違いと思ったら改修していくイメージです）

### Step 5: database connection and configuration

- まずGitで新たにトピックブランチを切りましょう
  - 以降、トピックブランチ上で作業をしてコミットをしていきます
- Bundlerをインストールしましょう
- `Gemfile` で `pg` （PostgreSQLのデータベースドライバ）をインストールしましょう
- `database.yml` の設定をしましょう
- `rails db:create` コマンドでデータベースの作成をしましょう
- `rails db` コマンドでデータベースへの接続確認をしましょう
- GitHub上でPRを作成してレビューしてもらいましょう
  - コメントがついたらその対応を行ってください。LGTM（Looks Good To Me）が2つついたらmasterブランチにマージしましょう

### Step 6: create the task model

タスクを管理するためのCRUDを作成します。
まずは名前と詳細だけが登録できるシンプルな構成で作りましょう。

- `rails generate` コマンドでタスクのCRUDに必要なモデルクラスを作成しましょう
- マイグレーションを作成し、これを用いてテーブルを作成しましょう
  - マイグレーションは1つ前の状態に戻せることを担保できていることが大切です！ `redo` を流して確認する癖をつけましょう
- `rails c` コマンドでモデル経由でデータベースに接続できることを確認しましょう
  - この時に試しにActiveRecordでレコードを作成してみる
- GitHub上でPRを作成してレビューしてもらいましょう

### Step 7: implement task creation, update and delete

- タスクの一覧画面、作成画面、詳細画面、編集画面を作成しましょう
  - `rails generate` コマンドでコントローラとビューを作成します
  - コントローラとビューに必要な実装を追加しましょう
  - 作成、更新、削除後はそれぞれflashメッセージを画面に表示させましょう
- `routes.rb` を編集して、 `http://localhost:3000/` でタスクの一覧画面が表示されるようにしましょう
- GitHub上でPRを作成してレビューしてもらいましょう
  - 今後、PRが大きくなりそうだったらPRを2回以上に分けることを検討しましょう

### Step 8: write feature specs for testing

- make the preperations for writing specs
	- prepare `spec/spec_helper.rb`, `spec/rails_helper.rb`
- write feature specs for task functions
- integrate CI tools such as Circle CI, and set Slack notifications
	- this is optional, but the mentor can add this for convenience
- recommended reading: https://leanpub.com/everydayrailsrspec

### Step 9: use Rails i18n to implement localization

- use Rails i18n to manage localized resources

\* doing so makes further steps (that display localized messages) easier to implement

### Step 10: set timezone for Rails

- set Rails' timezone to your local timezone

### Step 11: sort task index by created date

- tasks are sorted by ID now, let them be sorted by created date (asc and desc) too
- write feature specs to make sure the sorting works

### Step 12: validation

- validation setup
	- think about which columns need to be validated
	- add the appropriate database migrations
	- use `rails generate` to create basic migrations files
- display validation messages on the web page
- write model specs for the validations
- send a pull request to GitHub for code review

### Step 13: deploy

- masterブランチにシンプルなタスク管理システムができたので、デプロイしてみましょう。
- Herokuにデプロイを実施してみましょう
  - アカウントがなければ作成します
- デプロイされたHeroku上のアプリを触ってみよう
  - これからはこのアプリにタスクを登録して開発を進めましょう
  - ※ ただし、Herokuのアプリケーションはインターネットでどこでも参照できるので、公開してはまずい情報は載せないようにしましょう
    - Basic認証をこの時点でいれてもいいかもしれません
  - 今後、ステップが終わるたびにHerokuへ自分のアプリを継続的にデプロイしましょう
- デプロイの方法を `README.md` に記載しましょう
  - その際に、このアプリで使っているフレームワークのバージョン情報なども記載しておくとなおよいです

### Step 14: add due dates to tasks

- add due dates to tasks
- allow the task index to be sorted by due date
- write tests
- send a pull request, work with the code reviews, and deploy

### Step 15: add statuses to tasks, and make them searchable

- add statuses (todo, doing, done)
	- (optional) state machine gems are allowed if not newbie
- allow tasks to be searched by title and status on the index page
	- (optional) gems such as ransack are allowed if not newbie
- when searching, check the log to study the generated SQL statements
	- this is needed for further steps as well, and you should make it a habit
- 検索インデックスを貼りましょう
- add the appropriate model specs and feature specs

### Step 16: add priorties to tasks (\* skipable if trainee has related experience)

- add priorty to tasks (low, medium, high)
- sort tasks by priorty
- update feature specs
- send a pull request, work with the code reviews, and deploy (do this for every other step as well)

### Step 17: add pagination

- use the Kaminari gem and add pagination to the task index page

### Step 18: do some design

- use Bootstrap to make the application look better
	- (optional) write your own CSS to design

### Step 19: allow the application to be used by multiple users

- create the user model
- write a seed file to create the first user
- add relations to users and tasks
	- 関連に対してインデックスを貼りましょう
	- avoid N+1 queries
	- \* when deploying to Heroku, make sure the existing tasks will have relations to users (data maintenance)

### Step 20: implement login/logout features

- implement this yourself, without gems
	- by not using gems like Devise, trainees will have a better understanding how HTTP cookies and sessions work in Rails
	- they will also learn about authentication (such as how to handle passwords)
- implement the login page
- ensure that only logged in users can access task management
- show only tasks created by the user
- implement the logout function

### Step 21: implement user management pages

- add a management menu
- all management pages must have the `/admin` prefix
	- before you edit `routes.rb`, think about how you want to design the URLs and routing names (`*_path`)
- implement user index, create, update, delete features
- when a user is deleted, their tasks should also be deleted
- on the user index page, show how many tasks they have
- filter tasks by the author   

### Step 22: add roles to users

- users should be divided as admin users and general users
- user management pages are restricted to admin users only
- can set user role in user management
- should prevent deleting all admin users (at least have one admin)
- gem usage is optional

### Step 23: add labels to tasks

- allow tasks to be added with multiple labels
- tasks need to be searchable by labels

### Step 24: configure error pages

- customize the default Rails error pages
- serve different error pages circumstantially
	- at least for status code 404 and 500

## Postface

Congratulations, you have just completed the full curriculum!

Although the curriculum does not incude the following topics, they are also required for further training (usually on the job).

- Web application fundamentals
	- HTTP and HTTPS
- Rails advance usage
	- STI
	- logging
	- explicit transactions
	- asynchronous processes
	- asset pipeline (leaning on the deployment side)
- frontend, namely Javascript and CSS
- database
	- SQL
	- writing queries with better performance
	- index
- server side
	- Linux OS
	- web server (Nginx) configuration
	- application server (Unicorn) configuration
	- PostgreSQL configuration
- deployment tools
	- Capistrano
	- Ansible

## Extra (optional requirements)

In addition to the required steps, there are also optional requirements for the task management system. The trainee should check with their mentor on how to proceed with these.

### Optional Requirement 1: show an alert when a task nears its due date

- when the user logins, the system should show tasks that are near or past their due dates
- extra points for marking them as read/unread

### Optional Requirement 2: allow users to share tasks

- allow multiple users to read/edit the same tasks
	- e.g. sharing between mentor and trainee
- display the author name

### Optional Requirement 3: implement a user group function

- follow-up of the previous requirement
- able to set groups, and share tasks within the group

### Optional Requirement 4: allow file attachments to tasks

- allow file attachements to tasks
- Heroku: manage uploaded files with S3 bucket
- utilize the appropriate gems

### Optional Requirement 5: add avatars to users

- allow users to add an avatar image to their profile
- to speed up loading time, try to create thumbnails for the uploaded images
- utilize the appropriate gems and libraries

### Optional Requirement 6: add a task calendar

- to visualize due dates, categorize and display them on a calendar
- gem usage is optional

### Optional Requirement 7: allow tasks to be sorted by drag and drop

- add drag and drop sorting to the task index

### Optional Requirement 8: label usage graphs

- implement graphs to visualize data
- you should choose a graph format that is easy to read

### Optional Requirement 9: notify users by email of tasks nearing due date

- when a task is nearing its due date, send an email in the background to notify
- use cloud services to send mail
	- Heroku: SendGrid
	- AWS: Amazon SES
- send mail in batch, once daily
	- Heroku: Heroku Scheduler (addon)
	- AWS: cron job

### Optional Requirement 10: setup an AWS instance

- configure and deploy to AWS
- recommended middleware is nginx+Unicorn
- see server requirements for EC2 instances