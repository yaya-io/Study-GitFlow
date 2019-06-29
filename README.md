# Gitを使用した開発フロー
説明用のため開発に使用する以下のフローを記載


* GitHub Flow
* GitLab Flow 環境ブランチ戦略
* GitLab Flow リリースブランチ戦略

## 参考書籍
* GitLab 実践ガイド DevOpsワークフローの導入と運用 /著 北山 晋吾

  
## drawioについて
[draw\.io](https://www.draw.io/)
書籍の説明図をdrawioで作成

* ブラウザ上で各種フローや図を描くのに非常に便利
* 様々なアイコンやテンプレートを利用可能
* AWS系のアイコン等もあり
* SVG出力可(png,jpeg,pdfなども）
* Github,GoogleDrive,Dropboxなど各種サービスと直接連携
データの保存やエクスポート、インポートが可能

## GitHubFlow
![](./png/GitHubFlow.png)

GitHub Flowでは、機能ブランチ(Feature Branch)と Masterブランチ(Master Branch)のみを利用する。
1. Masterブランチから個別の機能修正や新機能実装といった名前の機能ブランチを作成してローカルで開発
1. 開発後に機能ブランチをローカルでコミットし、サーバー上の同盟のブランチにプッシュ
1. プッシュと同時にテストが行われ、レビューを行うためにPull Requestを作成
1. レビュー後にMasterブランチにマージし、動的にリリースする

## GitLab Flow 環境ブランチ戦略
![](./png/GitLabFlow_Env.png)

GitLab Flow(環境ブランチ戦略）は、環境ごとにブランチを用意し、各環境でのMergerequestが通ったものから、上位の環境に動的にデプロイを行う仕組み。
1. 機能開発するときは、Masterブランチから機能ブランチを作成して開発を行う
1. 開発後に、機能ブランチからMasterブランチに対してMergeRequestを作成する
1. Masterブランチをテスト環境へデプロイして確認を行う
1. MasterブランチからステージングブランチへのMergeRequestを作成し、マージと同時にステージングへのデプロイを行う
1. ステージングブランチから本番ブランチへのMergeRequestを作成し、マージと同時にリリースを行う


## GitLab Flow リリースブランチ戦略
![](./png/GitLabFlow_ReleaseBranch.png)

GitLab Flow(リリースブランチ戦略）は、ソフトウェアを開発するときに、リリースに対してブランチを用意する仕組み。
基本はMasterブランチ上（アップストリームバージョン)で新規機能開発を進め、バージョンごとに別ブランチを作成してリリースを行う。
各バージョンのブランチ内容は、そのバージョン内で閉じており、重大なバグフィックスだけをMasterブランチから取り入れていく。（アップストリームファーストポリシー）


