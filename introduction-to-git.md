---
marp: true
title: Git を使ったバージョン管理
theme: s2
headingDivider: 2
paginate: true
---

# <!-- fit --> Git を使ったバージョン管理

<!-- _class: lead -->
<!-- _backgroundImage: url(https://marp.app/assets/hero-background.jpg) -->

## Git とは？

- 分散型バージョン管理システム
- (主に)テキストファイルの編集履歴を管理
- Linux の生みの親であるリーナス・トーバルズが開発

## よくある問題

![bg right fit](https://raw.githubusercontent.com/yumenosora-system/introduction-to-git/master/assets/file-name-version.png)

- どれが最新かわからない！
- 誰が何を変えたのかわからない！

## Git を使えば

- 古いファイルを残す必要がない
  <i class="fa fa-arrow-right"></i> 最新のファイルがすぐに分かる
- 誰が何を変更したか分かる
- 古いバージョンに簡単に戻せる
- 複数人で同時に編集・統合できる

## <!-- fit --> Git ≠ GitHub

<!-- _class: lead -->

Git とは GitHub のことではない

## <i class="fab fa-git-alt"></i> Git と <i class="fab fa-github"></i> GitHub の違い

- Git: バージョン管理を行うためのアプリ
- GitHub: Git を使った開発支援サービス
  - リポジトリを提供
  - コードを全世界に公開可能
    - 非公開にもできる
  - プルリクエスト (プルリク、PR) などの独自機能

## <!-- fit --> インフラ担当者も<br>Git を覚える必要があるのか？

<!-- _class: lead -->

## <!-- fit --> Infrastructure as Code (IaC)

<!-- _class: lead -->

インフラはコード

## <!-- fit --> 手順書を元に手作業で構築<br><i class="fa fa-arrow-down"></i><br>手順をコード化して自動構築

<!-- _class: lead -->

## Git の流れ (1)

![bg](https://raw.githubusercontent.com/yumenosora-system/introduction-to-git/master/assets/git-flow1.svg)

## Git の流れ (2)

![bg](https://raw.githubusercontent.com/yumenosora-system/introduction-to-git/master/assets/git-flow2.svg)

## Git の流れ (3)

![bg](https://raw.githubusercontent.com/yumenosora-system/introduction-to-git/master/assets/git-flow3.svg)

## リポジトリとは？

- 「貯蔵庫」「収納庫」の意味
- ソースコード等の管理対象を溜めておく場所
- Git は分散型のため複数ある

## Git のインストール

- Windows: Git for Windows https://gitforwindows.org/
- CentOS 7: `yum -y install git`
- CentOS 8: `dnf -y install git`

## <!-- fit --> Git for Windows インストール時の注意 (1)

<!-- _class: font-size-small first-child-center -->

![Git for Windows インストール時の注意](https://raw.githubusercontent.com/yumenosora-system/introduction-to-git/master/assets/install-git-for-windows.drawio.svg)

他のオプションを選ぶと自動的に改行コードが変換され、毎回ファイル全体が変更点として認識されます。

## <!-- fit --> Git for Windows インストール時の注意 (2)

間違って改行コードを変換する設定を選んでしまったら…

    git config --global core.autocrlf false

で設定を修正し

    git config core.autocrlf

で <samp>false</samp> と表示されることを確認

## git config による設定の範囲

    git config --global core.autocrlf false

- --local: カレントディレクトリのリポジトリに対して設定
- --global: コマンドを打ったユーザーに対して設定
- --system: PCやサーバ全体に対して設定 (要管理者権限)

どこで設定されているか確認する場合は

    git config --show-origin core.autocrlf

## 名前とメールアドレスを設定

変更履歴に表示される名前を設定

    git config --global user.name "Your Name"

メールアドレスを設定

    git config --global user.email "you@example.com"

## Git の流れ (1)

![bg](https://raw.githubusercontent.com/yumenosora-system/introduction-to-git/master/assets/git-flow1.svg)

## リポジトリを作成してコミット (1)

1. `mkdir git-test` ディレクトリを作成
1. `cd git-test` 作成したディレクトリへ移動
1. `git init` ディレクトリをリポジトリとして初期化
1. ファイルを作成
1. `git status` 状態を確認
1. `git add .`
   カレントディレクトリのファイルをコミット対象へ追加

## コミット (commit) とは？

- 変更点に名前を付けてリポジトリへ保存すること
- 事前に `git add` でコミットする対象を指定しておく

## リポジトリを作成してコミット (2)

1. `git status` 状態を確認
1. `git commit -m "はじめてのコミット"`
   コメントを付けてコミット
   コメントは変更点がわかりやすいように書く
1. `git status` 再度状態を確認
1. `git log` 変更履歴を表示

## <!-- fit --> Windows で git log や git diff が文字化けする場合

以下のコマンドで環境変数を設定する

    SETX LANG ja_JP.UTF-8

設定後コマンドプロンプトを開き直す必要がある

## GitHub でリポジトリを作成

1. https://github.com/ を開く
1. サインインしていない場合は右上から <samp>Sign in</samp>
1. 左側の <samp>Repositories</samp> にある <samp>New</samp> をクリック
1. <samp>Repository name</samp> を入力
1. **Private** を選択
   ※ Public のままだと **全世界に公開される** ため注意
1. <samp>Create repository</samp> をクリック

## リポジトリにリモートリポジトリを設定

1. `git remote add origin https://github.com/xxx/xxx.git`
   でリモートリポジトリを追加
1. `git remote -v` で追加されたことを確認
1. `git push -u origin master` でリモートリポジトリへ反映
   `-u` を付けると既定のプッシュ先になる

## origin master とは？

origin

- デフォルトのリモートリポジトリの名前
- git は分散型のため複数のリモートリポジトリが設定可能

master

- デフォルトのブランチの名前

## ブランチとは？

開発の本流から分岐し、本流の開発を邪魔することなく作業を続ける機能

- リリース用ブランチ
- 機能追加用ブランチ
- バグ修正用ブランチ

などを `git branch` サブコマンドで作成できる

一般的にリリース用ブランチは master ブランチを使用する

## もう一度ファイルを編集

<!-- _class: font-size-small -->

1. ファイルを編集
1. `git diff` で差分を表示
1. `git status` で状態を確認
1. `git add -u`
   -u で更新されたファイルをコミット対象へ追加
1. `git commit -m "〇〇を追加"` でコミット
1. `git push` でリモートリポジトリへ反映
   既定のプッシュ先を設定したため、これだけで push できる

## GitHub の画面から変更履歴を確認する

1. リポジトリ名をクリック
1. 青い部分右側の <samp>commits</samp> をクリック
1. コミット時のコメントをクリック

## Git の流れ (2)

![bg](https://raw.githubusercontent.com/yumenosora-system/introduction-to-git/master/assets/git-flow2.svg)

## 他のユーザーをリポジトリへ招待

<!-- _class: font-size-small -->

1. GitHub のリポジトリ画面を開く
1. <samp>Settings</samp> > <samp>Manage access</samp>
1. <samp>Invite a collaborator</samp> をクリック
1. ユーザー名などを入力後 <samp>Add xxx to xxx</samp> をクリック
1. 招待されたユーザーへメールが送られる
1. 招待されたユーザーが招待を受け入れる
1. <samp>Manage access</samp> 画面に <samp>Collaborator</samp> として表示される

## クローンして編集

1. GitHub のリポジトリ画面を開く
1. 緑色の <samp>Code</samp> をクリック
1. <samp>Clone with HTTPS</samp> の部分に表示された URL をコピー
1. 先ほど作成したリポジトリとは別のディレクトリへ移動
1. `git clone https://github.com/xxx/xxx.git`
1. ファイルを編集

## コミットしてプッシュ

1. `git status`
1. `git add -u`
1. `git commit -m "○○を変更"`
1. `git push`
1. GitHub へ反映されているか確認

## push 時に rejected と表示された場合

- `git clone` してから `git push` するまでの間に他のユーザーが編集している場合発生
- `git pull` すれば自動で統合 (merge) されて解決する場合もある
- `git pull` しても <samp>Automatic merge failed</samp> と表示される場合は手作業で修正する

## git init しなくても良い

GitHub でリポジトリを作成後 `git clone` すれば `git init` でのローカルリポジトリ作成は不要

## <!-- fit --> 毎回ユーザー名/パスワードを求められる場合

SSH キーを作成し、SSH URL を使ってクローンすることで回避可能

事前に GitHub へ SSH キーを登録しておく必要がある

## SSH キーを作成し GitHub へ登録

1. `ssh-keygen -t rsa` で SSH キーを作成
1. https://github.com/ を開く
1. サインインしていない場合は右上から Sign in
1. 右上のアイコン > Settings
1. 左のメニュー > SSH and GPG keys
1. New SSH key
1. Title に名前、Key に作成した id_rsa.pub の内容をコピペ

## SSH URL を使ってクローン

1. GitHub のリポジトリ画面を開く
1. 緑色の <samp>Code</samp> をクリック
1. <samp>Use SSH</samp> をクリック
1. <samp>Clone with SSH</samp> の部分に表示された URL をコピー
1. `git clone git@github.com:xxx/xxx.git`

## Git の流れ (3)

![bg](https://raw.githubusercontent.com/yumenosora-system/introduction-to-git/master/assets/git-flow3.svg)

## プルして編集

1. 最初に作成したリポジトリのディレクトリへ移動
1. `git pull` でリモートリポジトリから差分を取得
1. ファイルを編集

## コミットしてプッシュ

1. `git status`
1. `git add -u`
1. `git commit -m "○○を変更"`
1. `git push`
1. GitHub へ反映されているか確認

## .gitignore



## GUI で操作可能なツール

- Visual Studio Code https://code.visualstudio.com/
- GitHub Desktop https://desktop.github.com/
- TortoiseGit https://tortoisegit.org/

## 終わり

<!-- _class: lead -->
