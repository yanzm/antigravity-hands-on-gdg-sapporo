# Antigravity ガイド

ハンズオンで使う Antigravity について、知っておくと便利な情報をまとめています。

<span style="color:salmon"><b>※ このドキュメントの内容は 2026/03/12 時点の情報です。Antigravity は活発にアップデートされているため、最新の情報は公式ドキュメント ( https://antigravity.google/docs ) を確認してください。</b></span>

## Antigravity とは

Antigravity は Google が提供するエージェント型開発プラットフォームです。従来のコーディングアシスタントとは異なり、計画、コーディング、ウェブ閲覧が可能な自律型エージェントを管理する「ミッション コントロール」を提供します。

公式サイト : https://antigravity.google/

公式ドキュメント : https://antigravity.google/docs

> **コラム : Gemini 3.1 Pro が使えるようになりました**
>
> Antigravity で最新の Gemini 3.1 Pro モデルが利用可能になりました。会話開始時のモデル選択で Gemini 3.1 Pro を選ぶことができます。より高精度なコード生成や計画立案が期待できるので、ぜひ試してみてください。
>
> 詳しくはこちら : https://antigravity.google/blog/gemini-3-1-pro-in-google-antigravity


## レートリミットとクォータ

Antigravity にはプランに応じた利用量の上限（クォータ）とレートリミットがあります。

すべてのプランで以下が利用できます：

- Gemini 3.1 Pro、Gemini 3 Flash などのモデル
- 無制限の Tab 補完と Command リクエスト
- Agent Manager、Browser など全機能へのアクセス

### プランごとの違い

| プラン | クォータ | リフレッシュ |
| --- | --- | --- |
| Google AI Ultra / Workspace AI Ultra for Business | 最大のクォータ | 5時間ごと（週間制限なし） |
| Google AI Pro | 高いクォータ | 5時間ごと（週間上限あり） |
| 無料（Pro / Ultra なし） | 基本クォータ | 週ごと |

レートリミットはエージェントが行った作業量に比例します。簡単なタスクなら多くのプロンプトを送れますが、計画＋複数ファイル編集＋テストのような大きなタスクは消費が大きくなります。

AI Pro / Ultra プランではクォータを使い切った後に AI クレジットで追加利用することもできます。

詳しくはこちら : https://antigravity.google/docs/plans

### クォータを節約するコツ

- アイデア出しや調べものなど、エージェントの開発機能が不要な作業は Google AI Studio など別のツールで行う
- 1つの会話で多くのことをやりすぎず、タスクを分けて会話を開始する
- 簡単な修正には Fast モードを使う
- プロンプトは具体的に書く（やり直しが減る）


## エージェント マネージャー

Antigravity を起動すると、ファイルツリーではなく「エージェント マネージャー」というミッション コントロール画面が表示されます。

- **Open Folder** : ローカルフォルダを開きます
- **Open Agent Manager** : エージェント マネージャーを開きます
- **Clone Repository** : Git リポジトリをクローンします
- **Workspaces** : 過去に開いたワークスペースの一覧です


## 会話モード（Conversation mode）

会話を開始する際に、2つのモードを選択できます。

- **Planning** : 詳細な調査や複雑なタスクに向いています。思考予算を多く使います。エージェントが Implementation Plan や Task List を作成してから実装に入ります
- **Fast** : 簡単なタスク向け。速度優先で、計画フェーズを省略して素早く応答します


## アーティファクト

エージェントが作業する際に生成する成果物です。

- **Task List** : 構造化されたタスクリスト。編集やコメントが可能です
- **Implementation Plan** : 変更の設計と技術詳細
- **Walkthrough** : 実装完了後の変更概要とテスト方法
- **Code diffs** : コード変更の詳細。レビューやコメントが可能です
- **Screenshots** : UI 変更前後のキャプチャ
- **Browser Recordings** : 動的インタラクションのビデオ

アーティファクトにはコメントを追加でき、Google ドキュメントのようにエージェントにフィードバックを送ることができます。


## エディタ

VS Code に近い操作感のエディタが内蔵されています。

- エージェント マネージャーとエディタの切り替え : `Cmd + E`（Mac）/ `Ctrl + E`（Windows）
- ターミナルパネルの表示 : `` Ctrl + ` ``
- エージェントパネルの表示 : `Cmd + L`（Mac）/ `Ctrl + L`（Windows）

### 予測入力

コード入力時にスマート自動補完が表示されます。**Tab** キーで受け入れます。

### インラインコマンド

`Cmd + I`（Mac）/ `Ctrl + I`（Windows）で、自然言語でインライン補完をリクエストできます。エディタ上でもターミナル上でも使えます。


## ルール

エージェントの動作をガイドする指針です。コード生成時に適用されます。

- **グローバルルール** : すべてのプロジェクトに適用。`~/.gemini/GEMINI.md` に保存されます
- **ワークスペースルール** : 特定のプロジェクトにのみ適用。`your-workspace/.agents/rules/` に保存されます

Antigravity の UI からは、**...** → **Customizations** → **Rules** で設定できます。

ルールの例：

```
* PEP 8 スタイルガイドに準拠すること
* すべてのメソッドにドキュメンテーションコメントを書くこと
* 日本語でコメントを書くこと
```


## ワークフロー

よく使うプロンプトを保存しておき、`/` で呼び出すことができるオンデマンドの機能です。

- **グローバルワークフロー** : `~/.gemini/antigravity/global_workflows/<NAME>.md`
- **ワークスペースワークフロー** : `your-workspace/.agents/workflows/`

ワークフローの例（単体テスト生成）：

```
* Generate unit tests for each file and each method
* Make sure the unit tests are named with test_ prefix
```


## スキル

「必要になるまで休眠状態にある専門知識パッケージ」です。プロンプトに含めず、リクエストがメタデータと一致した場合のみ読み込まれます。

スキルのディレクトリ構成：

```
my-skill/
├── SKILL.md      # メタデータと指示（必須）
├── scripts/      # Python または Bash スクリプト（オプション）
├── references/   # テキスト/ドキュメント/テンプレート（オプション）
└── assets/       # 画像やロゴ（オプション）
```

- **グローバルスキル** : `~/.gemini/antigravity/skills/`
- **ワークスペーススキル** : `<workspace-root>/.agents/skills/`


## ブラウザ

Antigravity には Chrome 統合のブラウザサブエージェントがあります。エージェントが Web ページを閲覧して情報を収集したり、動作確認を行ったりできます。

利用可能なツール：
- クリック、スクロール、入力
- コンソールログ読み取り
- DOM キャプチャ、スクリーンショット
- ビデオ撮影


## エージェント保護

### ターミナル実行ポリシー

| モード | 説明 |
| --- | --- |
| Off | 明示的に許可したコマンド以外は実行しない（最も安全） |
| Auto | 内部の安全性モデルで判断し、リスクの高いコマンドは許可を求める |
| Turbo | 明示的に拒否したコマンド以外は実行する（最も高速だがリスクも高い） |

許可リスト（Off モード）や拒否リスト（Turbo モード）でコマンドを細かく制御できます。

### ブラウザセキュリティ

`~/.gemini/antigravity/browserAllowlist.txt` で、エージェントがアクセスできるドメインを制限できます。


## 参考資料・コンテンツ

- Antigravity 公式サイト : https://antigravity.google/
- Antigravity 公式ドキュメント : https://antigravity.google/docs
- Antigravity ユースケース : https://antigravity.google/use-cases
- Getting Started Codelab : https://codelabs.developers.google.com/getting-started-google-antigravity?hl=ja
- YouTube チャンネル : https://www.youtube.com/@googleantigravity
