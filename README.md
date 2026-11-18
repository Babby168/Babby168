# Tatsumi Baba（馬場 巽 / Babby）

広告映像制作会社で約3年半、テレビCMやWeb動画の制作進行を担当しました。現在はRuby on Railsを軸に、Webエンジニアへの転職活動中です。

個人開発の「PieceFit」を企画・設計から公開まで一人で手がけ、公開後も運用と改善を続けています。

## 🧩 PieceFit

**BATTLE OF RUNTEQ vol.7 部門賞（技術力）受賞**

PieceFitは、デスクワーカー向けのストレッチ習慣化アプリです。首・肩・腰から気になる部位を選び、約1分のストレッチをするとピースを獲得できます。続けるうちにモザイクアートが完成し、取り組んだ成果がコレクションとして残ります。

ログインなしで、部位の選択からストレッチまで試せます。

[アプリを試す](https://piecefit.app) · [ソースコード](https://github.com/Babby168/PieceFit) · [大会公式ページ](https://battleof.runteq.jp/)

### 実装で工夫したこと

**モザイクアートの進捗表示と、完成画像の生成を分けました。**

- 進捗はHTML/CSSグリッドで表示し、ピースを獲得するたびに画像を生成する処理を省きました。
- 完成時はlibvipsで1枚の画像に合成し、Cloudinaryに保存します。合成とアップロードをSolid Queueでバックグラウンド実行することで、ユーザーが処理の完了を待たずに画面を操作できるようにしました。

画像処理の非同期化は、まず[検証用リポジトリ](https://github.com/Babby168/for-images_dev)でSidekiqとRedisを使って試しました。PieceFit本体では、すでに導入されていたSolid Queueで実現できると判断し、Redisの構築・運用を追加せずに済む構成にしました。

### 品質と公開後の改善

- **ピースの二重獲得防止** × 同時にリクエストが届いても二重に獲得しないよう、`with_lock`で排他制御しています。
- **テストと本番運用** × RSpecでテストを書き、RuboCop・Brakeman・Bundler Auditでチェックしています。本番エラーはSentryで監視し、画像処理ジョブには一時的な失敗に備えて再試行を設定しています。
- **ユーザーの声を受けた改善** × 「アートの完成までに時間がかかる」という声を受け、最初の作品を少ないピース数で完成できる仕組みを検討しています。

**初回公開までの開発期間**　2026年6〜8月（約2か月）

## About

前職では、クライアント・監督・技術スタッフなど立場の異なる関係者の間に入り、制作進行・予算・スケジュールを管理していました。次の工程で必要な情報や確認事項を先回りして整理し、複数の案件を納期まで進めてきました。

この進め方をPieceFitの開発にも活かしています。機能をIssueに分解し、GitHub Projectsで計画と実績を日々確認しながらスケジュールを調整しました。変更の経緯を追えるよう、Issue単位でブランチを作り、プルリクエストに変更内容を記録しました。

- **学習**　RUNTEQでRuby on Railsを中心に学習（2025年12月〜2026年9月）
- **興味のある領域**　ユーザーに直接届くWebサービス、エンターテインメント、映像・メディア

## 主な使用技術

| 分野 | 技術 |
| --- | — |
| Web開発 | Ruby / Ruby on Rails 8.1 / PostgreSQL / Hotwire（Turbo・Stimulus） |
| UI | Tailwind CSS / daisyUI |
| 非同期処理・画像処理 | Active Job / Solid Queue / libvips / Cloudinary |
| 開発・本番環境 | Docker / Render / Neon |
| テスト・品質 | RSpec / RuboCop / Brakeman / Bundler Audit / Sentry |

実装方針の整理や技術選定の壁打ちにはCursorやClaudeなどを使っています。提案された内容は、必要に応じて公式ドキュメントで確認し、実装内容と採用理由を自分で説明できる状態にしてから取り入れています。

## 技術記事・登壇

Railsの実装でつまずいた点や、Web開発で学んだことを記事やLTで発信しています。

[Qiita](https://qiita.com/Babby) · [note](https://note.com/bby)

<details>
<summary>学生時代の活動</summary>

- 青山学院大学 地球社会共生学部で、デジタルファブリケーションを用いた地理空間情報の表現を研究しました。[卒論リポジトリ](https://github.com/furuhashilab/2021gsc_TatsumiBaba)
- TEDxAoyamaGakuinU 2020では、撮影・編集・演出チームのリーダーとして、オンライン開催への切り替えを主導しました。

</details>
