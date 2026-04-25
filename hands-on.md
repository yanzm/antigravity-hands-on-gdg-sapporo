# 「札幌 × 桜」をテーマにした Web アプリを Antigravity で作ろう

〜自律型AIエージェントで体験、次世代の爆速プロトタイピング〜

講師 : あんざいゆき ( https://x.com/yanzm )

普段は Android アプリを開発するお仕事をしています。最近は AI に個人開発アプリの実装を手伝ってもらったり、自分用の便利ツールを作ってもらったりしてます。めっちゃ楽しいです。

## スケジュール

| 時間 | 内容 |
| --- | --- |
| 13:40 - 14:00 | セットアップ（事前準備の確認、Gemini の設定、[無料トライアルクレジット](setup-free-trial.md)） |
| 14:00 - 16:00 | 「札幌 × 桜」をテーマにした Web アプリを Antigravity で作ろう |
| 16:00 - 17:00 | 質問タイム＆成果発表＆休憩 |

## このセッションの目標

**「完璧な設計図を作ること」ではなく、「AIと一緒にざっくり作って、動くものを見ながら手直ししていく」** という次世代の開発体験を味わうことです。細かいエラーや実装方法はすべて Antigravity に任せて、あなたは **「開発のディレクター」** としてアプリを育てていきましょう！

## Antigravity とは

[Antigravity](antigravity-guide.md#antigravity-とは) は Google が提供するエージェント型開発プラットフォームです。今日はこれを使って、Webアプリのアイデア出しから実装、そして公開（デプロイ）まで体験しましょう。

## セットアップ

### 事前準備の確認

以下の準備ができているか確認してください。

- [ ] 個人の Google アカウント（@gmail.com）を持っている
- [ ] ノートPC に Antigravity がインストールされている（ダウンロード : https://antigravity.google/download ）
- [ ] Google Chrome 最新版がインストールされている

<span style="color:salmon"><b>まだの方は手をあげて教えてください！</b></span>

### Antigravity に Google アカウントでログイン

1. Antigravity を起動します。初回起動時はオンボーディングウィザードが表示されます。

![Welcome to Antigravity](images/image49.png)

VS Code などの設定を引き継ぎたい方は Import を選択してください。そうでない方は Start fresh のままで OK です。

![Choose setup flow — 「Start fresh」のまま Next](images/image50.png)

好きなテーマを選んでください。これ以外のテーマもあり、あとで変更できます。

![Choose an editor theme type — お好みのテーマを選んで Next](images/image51.png)

Recommend を選択してください。

![Agent の使い方 — 「Review-driven development」（RECOMMENDED）のまま Next](images/image52.png)

デフォルト選択のまま進めてください。

![Configure Your Editor — デフォルトのまま Next](images/image53.png)

2. **Sign into Google** の画面で **Sign in with Google** をクリックして、個人の Google アカウントでログインします

![Sign into Google](images/image54.png)

3. 利用規約に同意して **Next** をクリックします

![Terms of Use — 利用規約に同意して Next](images/image55.png)

4. オンボーディングが完了するとエディタが表示されます

> **Note** : オンボーディングでログインをスキップした場合は、エディタ右上の **Log in →** ボタンからログインできます。

![Antigravity 起動画面](images/image1.png)


### Gemini の設定

Antigravity が使う Gemini のグローバルルールを設定します。

1. エディタモードで右上の右パネルボタンをクリックし、Agent パネルを開きます

![... メニューから Customization を選択](images/image24.png)

2. 右上の **...** をクリックし、**Customization** を選択します

![... メニューから Customization を選択](images/image3.png)

3. **Rules** タブを選択します

4. **+ Global** ボタンをクリックして、グローバルルールを追加します

![Rules タブの + Global ボタン](images/image4.png)

5. 以下の内容を入力します

```markdown
* Antigravity の python のプロジェクトは常に virtual environment を利用すること
* Antigravity の Task や Plan は必ず日本語で記述すること
```

![グローバルルールの入力](images/image5.png)

このルールを設定しておくと、Antigravity のエージェントが Python プロジェクトで仮想環境を使うようになり、タスクやプランが日本語で表示されるようになります。

＊ グローバルルールは `~/.gemini/GEMINI.md`（Windows の場合は `%USERPROFILE%\.gemini\GEMINI.md`）に保存されます。


### 無料トライアルクレジットの設定

[無料トライアルクレジットのセットアップ](setup-free-trial.md) の手順に従って、Google Cloud の請求先アカウントとプロジェクトを作成してください。



## ステップ 1 : AI Studio で「壁打ち」してアイデアを決める（目安：15分）

事前に作りたいものが決まっていなくても問題ありません。まずは AI に「ざっくりとした問い」を投げかけて、壁打ちしながらアイデアを生み出すところからスタートします。

> **Tip** : セットアップで作成した Google Cloud プロジェクトで Gemini API Key を発行すれば、アプリ内に Gemini を使った AI 機能（チャット、レコメンド、テキスト生成、画像生成、音声合成など）を組み込むこともできます。もちろん AI 機能を使わないアプリでも全然 OK です！

このステップでは Antigravity の[クォータ](antigravity-guide.md#レートリミットとクォータ)を節約するため、Google AI Studio を使います。

### Google AI Studio で会話を開始する

Google AI Studio ( https://aistudio.google.com/ ) にアクセスします。ログインが必要な場合は Google アカウントでログインしてください。

左サイドバーの「Playground」から新しいチャットを開始します。

![Google AI Studio](images/image6.png)

以下のようなプロンプトを入力してみましょう。最初の3行は **自分の情報に書き換えて** ください。取り入れたい要素は例にないものでも全然OKです。自由に書いてみてください。

```
私が好きなもの／好きな過ごし方：（例：お花見、写真撮影、カフェ巡り、北海道グルメ、ランニング…）
アプリを使うシーン：（例：一人で散歩中 / 友達とお花見 / 家族で観光 / 子供と週末 / 旅行者として / 地元民として…）
アプリの雰囲気：（例：かわいい / ゲーム的 / 実用的 / エモい・ノスタルジック / クール / ネタ寄り…）
取り入れたい要素（いくつでも）：地図 / GPS / カメラ / クイズ / AI（チャット・画像生成など） / 音声 / スタンプラリー / 写真比較 / おみくじ / ランダム

札幌の「桜（お花見・桜の名所めぐり）」をテーマにしたWebアプリを作りたいです。
上の情報をふまえて、現地を訪れた人が思わず使いたくなるようなアプリのアイデアを3つ提案してください。

【アイデアの制約条件】
* たった2時間のワークショップで、AIを使って完成させられる「シンプルで単機能」なものにしてください。
* 複雑なユーザー登録（ログイン機能）、高度な3D/AR機能、壮大なゲームシステム、ユーザー同士のSNS機能は一切不要です。
* ブラウザでサクッと動く、ミニマムだけど「実際に札幌の街で桜を楽しむのが楽しくなる」アイデアをお願いします。

【出力フォーマット】
それぞれのアイデアに、以下を添えてください：
* アプリ名（キャッチーなもの）
* 一言コンセプト
* ざっくりした画面構成（どんな画面が何枚くらい必要か）
```

![Google AI Studio でプロンプトを入力](images/image7.png)

AIが提案してくれたアイデアの中から、気に入ったものを選びましょう。もちろん、自分のアイデアがある方はそれでもOKです。

> **壁打ちのコツ** : ピンとくるものがなければ「別のアイデアをもう3つ出して」と追加提案を求めたり、「2番目のアイデアの○○の部分が面白い。それを活かした別のアプリを3つ提案して」のように一部を採用して深掘りするのも効果的です。遠慮なく何度もやりとりしましょう。

### アイデアを具体化する

アイデアが決まったら、さらに具体的にしていきます。

```
「○○」（選んだアイデア）を作りたいです。
たった2時間のハンズオンで完成できるシンプルな構成で、具体的な機能要件をまとめてください。

- メインの機能（1〜2個に絞る）
- 画面構成（1〜3画面程度）
- 使うデータ（場所、画像、説明文など）
- 札幌ならではの面白いポイント
- ワークショップ会場でも全機能を試せるようにするための工夫（GPS系の機能がある場合など）
```

> **Note** : AI が具体的な技術スタックや実装戦略まで提案してくることがありますが、実装は Antigravity に任せるので気にしなくて大丈夫です。大事なのは「何を作るか」の要件がまとまっていることです。

要件がまとまってきたら、最後に AI エージェントに渡すためのプロンプトにまとめてもらいましょう。

```
ここまでの内容を踏まえて、AIエージェント（Antigravity）にWebアプリの実装を指示するためのプロンプトを作成してください。

プロンプトには以下を含めてください：
- 作るアプリの概要と目的
- 機能の具体的な仕様（何を入力したら何が起きるか）
- 画面構成とUIのイメージ（レイアウト、色、雰囲気）
- 使用するデータ（そのまま使えるJSON等の形式で）
- 技術的な指定があれば（地図ライブラリ、APIなど）

出力はプロンプト本文のみ。「以下をコピーしてください」等の前置きや、説明・補足は不要です。
```

AI Studio の回答の **⋮** メニューから「**Copy as markdown**」を使ってコピーすると、書式を保ったまま貼り付けられます。

![Copy as markdown](images/image12.png)

> **Note** : AI Studio がプロンプト本文以外に説明やヒントも一緒に出力することがあります。Antigravity に渡すのは **プロンプト本文の部分だけ** にしましょう。余計な説明が混ざると、エージェントが混乱する原因になります。

このプロンプトをステップ 2 で Antigravity に渡します。



## ステップ 1.5 : Stitch で UI のイメージを作る（任意・目安：10分）

Google Labs の AI UI デザインツール [Stitch](https://stitch.withgoogle.com/) で、アプリの見た目のイメージを先に作っておくと、ステップ 2 で Antigravity にデザインの雰囲気を伝えやすくなります。興味がある方はやってみましょう。時間がない場合はスキップして **ステップ 2 に進んで OK** です。

> **Note** : Stitch は実験的なサービスです。当日利用できなかったり生成に待ち時間が発生する場合があるので、うまく動かないときはスキップして大丈夫です。

### Stitch にアクセスする

[Stitch](https://stitch.withgoogle.com/) にアクセスし、Google アカウントでログインします。Web アプリを作るので **Web** モードを選択します。

### UI を生成する

入力欄に **ステップ 1 で作成したプロンプト（Antigravity に渡す用のもの）をそのまま貼り付けて** 送信します。

![Stitch](images/image56.png)

最初の結果を土台にして、以下の2つの機能で素早く調整できます。ゼロから作り直すよりこちらを使うのがおすすめです。

- **Create Variant（バリエーション生成）** : ツールバーの AI アイコンのメニューの中の **バリエーション** ボタンから、既存デザインを残したまま別パターンを横に並べて生成します。「別の方向性も見てみたい」ときに、前の結果を失わずに試せます
- **チャットで部分修正** : チャット入力欄に「ヘッダーをもっと大きくして」「カードを横並びに」「色を桜色に寄せて」のように自然言語で指示すると、気に入った部分は保持したまま指定箇所だけが更新されます

![AIメニュー](images/image57.png)

![バリエーション](images/image58.png)

![バリエーション結果](images/image59.png)

### Antigravity に渡す

生成した UI を Antigravity に参考として渡す方法は2つあります。

- **スクリーンショットで渡す** : 一番簡単。気に入った画面のスクリーンショットを撮り、ステップ 2 で Antigravity にプロンプトと一緒に添付します
- **コードをコピーして渡す** : Stitch の **Export** メニューから **コードをクリップボードにコピー** を選び、ステップ 2 で Antigravity に渡すプロンプトの末尾に貼り付けて「このデザインを参考に実装してください」と添えます

![エクスポート](images/image60.png)

> **Tip** : 参加者ごとに違った雰囲気の UI が生まれて成果物に個性が出ます。完璧なデザインを作ろうとせず、Antigravity への「ヒント」くらいの気持ちで使うのがおすすめです。



## ステップ 2 : Antigravity で最初のプロトタイプを作らせる（目安：10分）

アイデアが固まったら、いよいよ Antigravity を使ってアプリを作っていきます。

### Antigravity の画面構成

Antigravity には Editor ウィンドウと Agent Manager ウィンドウがあります。

#### Editor ウィンドウ

Editor ウィンドウは VS Code をフォークしたエディターです。
右上の Open Agent Manager ボタンで Agent Manager ウィンドウを開くことができます。

![Editor ウィンドウ](images/image19.png)

左にファイル エクスプローラなど、下にターミナル、右にエージェントパネルが表示されます。
右上のボタンで各パネルの表示・非表示を切り替えられます。

![Editor ウィンドウのパネル](images/image20.png)


#### Agent Manager ウィンドウ

Agent Manager ウィンドウでは、複数のエージェントをまとめて管理できます。異なるワークスペースのエージェントを一覧で確認したり、同じワークスペースに対して複数のエージェントを同時に動かすこともできます。
右上の Open Editor ボタンから Editor ウィンドウを開くことができます。

> **Note** : 同じワークスペースで複数のエージェントを同時に動かす場合、同じファイルを編集しようとすると競合が発生します。競合を避けるには、それぞれのエージェントが異なるファイルを担当するようにするか、リポジトリを別の場所にクローンしたり、git worktree で作業ディレクトリを分けて別々のワークスペースで作業させるといった方法があります。

![Agent Manager ウィンドウ](images/image21.png)


### Agent との会話を開始する

Agent との会話は Editor ウィンドウ, Agent Manager ウィンドウどちらでも可能です。ここでは Agent Manager ウィンドウで開始してみましょう。

左上の Start new conversation をクリックすると、新しい会話を開始する画面になります。

![Start new conversation](images/image25.png)


ワークスペースを開いていないので、Workspaces に選択肢がありません。

![New conversation in](images/image26.png)


先にワークスペースを作りましょう。左の Workspace のところの + ボタンをクリックします。

![ワークスペース追加](images/image27.png)

Open Folder をクリックして、新しくこのアプリ用のフォルダを作ってそこを開きます。（例 : `~/Projects/my-sapporo-app`）

![ワークスペース追加](images/image28.png)

「Do you trust the authors of the files in this folder?」というダイアログが表示されたら「Yes, I trust the authors」をクリックします

![信頼確認ダイアログ](images/image11.png)

左側の Workspace の下に開いたフォルダが表示され、新しい会話を始める対象も追加したワークスペースになります。

![ワークスペース追加](images/image29.png)


入力欄の下にある + ボタンのメニューから **Plan** を有効にできます。

![Planモード選択](images/image9.png)

- **Plan** : エージェントが Implementation Plan（実装計画）を作成してからユーザーの承認を経て実装に入ります。詳細な調査や複雑なタスクに向いています。Plan を有効にしないと、計画フェーズを省略して即実装に入ります（簡単なタスク向き）

モデルは Gemini 以外にも Claude や GPT-OSS なども選択できます。

![モデル選択](images/image10.png)

今回はアプリを一から作るので、**Plan** を有効にして、モデルは **Gemini 3.1 Pro (High)** を選択しましょう。

> **Note** : モデルが limit に達したというメッセージが表示された場合は、別のモデルに切り替えて試してみてください。

### エージェントにアプリの作成を依頼する

ステップ 1 で作成したプロンプトを Agent パネルに貼り付けて送信しましょう。

![プロンプト入力](images/image30.png)

1.5 で Stitch にデザインを作成させた場合は、コピーしたコードもプロンプトの最後に追加します。

![Stitchのコードもプロンプト入力](images/image61.png)


エージェントが **Implementation Plan**（実装計画）を作成してくれます。

![Implementation Plan](images/image14.png)

### 計画をレビューする

エージェントが作成した計画をざっと確認しましょう。大きな方向性が合っていれば OK です。細かい修正はステップ 3 のイテレーションでいくらでもできるので、ここで完璧にする必要はありません。

- **Implementation Plan** : 変更の設計と技術詳細が書かれています

もし気になる点があれば、チャットでフィードバックを送ったり、Implementation Plan の特定の行にコメントを付けることもできます。行の横にある **+** ボタンをクリックするとコメント欄が開きます。

![Comment on this line](images/image15.png)

![コメントを追加](images/image16.png)

> **Tip** : 計画で採用されている技術スタック（フレームワークやライブラリなど）に詳しくなくても大丈夫です。「使っている技術について初心者向けに解説して」「各ライブラリの役割をドキュメントにまとめて」とエージェントに頼めば、学習用の資料も作ってくれます。

納得したら **Proceed** をクリックして、エージェントにコーディングを開始してもらいましょう。

![Proceed](images/image31.png)

エージェントがコードの生成を開始します。ブラウザで自動的に動作確認を行う場合もあります。しばらく観察してみてください。


### コマンド実行の許可

エージェントがコーディングを開始すると、ターミナルでコマンド（パッケージのインストールやサーバーの起動など）を実行しようとします。このとき「Run command?」や「Send command input?」というダイアログが表示されることがあります。

![Run command?](images/image18.png)

![Send command input?](images/image32.png)

内容を確認して問題なければ **Run** や **Accept** をクリックしましょう。毎回確認するのが面倒な場合は、[エージェント保護](antigravity-guide.md#エージェント保護)の設定でターミナル実行ポリシーを変更できます。

### 完成を確認する

実装が完了すると、Antigravity は作業報告として **Walkthrough** を作成します。エージェントが実行した作業内容は **Task List** として Walkthrough と一緒に表示されます。

![Walkthrough](images/image33.png)

この Walkthrough には動作確認を行う方法が書かれているので試してみましょう。この例では「npm run dev でローカルサーバーを起動し、ブラウザで動作をご確認ください。」とあるので、Editor ウィンドウのターミナルでやります。

右上の Open Editor ボタンで Editor ウィンドウを開きます。

![Agent Manager の Open Editor ボタン](images/image34.png)

右上の Toggle panel ボタンで下のパネルを開き、Terminal が選択されていることを確認します。

![ターミナルパネルを開く](images/image35.png)

Terminal に

```
npm run dev
```

と入力して Enter します。

![npm run dev の実行](images/image36.png)

表示された Local のアドレスをブラウザで開きます。（ q + Enter で起動したローカルサーバーが終了します）

![ブラウザでアプリを確認](images/image37.png)

> **Note** : 成果物が `index.html` だけのシンプルな構成だった場合、Walkthrough には「ブラウザで `index.html` を開いてください」のような指示が書かれていることが多いです。Antigravity のファイルエクスプローラで `index.html` を右クリック → **Reveal in Finder**（Mac）/ **Reveal in File Explorer**（Windows）→ Finder/Explorer 上でダブルクリックすると、既定ブラウザで開けます。
>
> ただし、JSON をローカルから読み込んだり ES モジュール (`import`) を使ったりするアプリは、この方法だと CORS エラーで動きません。その場合は Antigravity のターミナルで以下を実行し、ブラウザで `http://localhost:8000/` を開いてください。
>
> ```
> python3 -m http.server 8000
> ```
>
> Windows では `py -m http.server 8000` を使います。

最初のプロトタイプが動きました！ここからはステップ 3 で、自分の目で確認しながら改善を繰り返していきます。


## ステップ 3 : 動くものを見て直す「超高速イテレーション」（目安：60分）

### クォータ節約のための指示を追加する

Antigravity ではエージェントがブラウザで自動検証することがあります。しかしこの機能はクォータの消費量が多いため、ここからのイテレーションでも毎回ブラウザ検証が走るとクォータを大量に消費してしまいます。無料ユーザーはクォータが限られているので、ワークスペースの[ルール](antigravity-guide.md#ルール)を追加して動作確認を自分で行うようにしましょう（詳しくは「[クォータ節約＆開発のコツ](#クォータ節約開発のコツ)」を参照）。

> **Note** : 本来はグローバルルールと同様に UI（**...** → **Customization** → **Rules** → **+ Workspace**）から追加できますが、バージョン 1.20.3 から「no workspaces found」エラーで追加できないバグがあります（[参考1](https://discuss.ai.google.dev/t/customizations-panel-empty-no-workspaces-found-error-after-1-20-3-update/129738/16)、[参考2](https://discuss.ai.google.dev/t/add-workspace-rule-failed/114582)）。ここではターミナルから手動でファイルを作成します。

Editor ウィンドウのターミナルで以下のコマンドを実行して、ルールファイルを作成します。

```
mkdir -p .agents/rules && touch .agents/rules/save-quota.md
```

![ルールファイル作成](images/image39.png)

作成した `save-quota.md` をエディタで開くと、ルール専用の編集 UI が表示されます。

![ルール編集 UI](images/image38.png)

- **Activation Mode** : 「Always On」を選択
- **Content** : 以下を入力

```
AIのQuota（利用制限）を節約するため、ユーザーが明示的に指示しない限り、自律的なブラウザの起動や画面の視覚的な確認は行わないでください。動作確認はユーザーが行います。コードの修正のみを高速に行ってください。
```

ルールファイルを保存したら、エージェントに新しい会話で指示を送る際にこのルールが自動的に適用されます。

### モデルを切り替える

クォータを節約するため、モデルを **Gemini 3 Flash** に切り替えましょう。Flash は応答が速く、クォータの消費も少ないので、細かい修正を繰り返すイテレーションに向いています。あわせて **Plan は無効** にして、計画フェーズを省略して即修正してもらうようにしましょう。

### イテレーションを始める

**新しい会話を開始** して修正を依頼していきます。ブラウザでアプリを確認して気になった点をエージェントに伝えましょう。

```
以下の点を修正してください。
- ヘッダーの色をもう少し落ち着いた色にしてください
- フォントサイズを少し大きくしてください
```

スクリーンショットを撮って、画像と一緒に具体的にコメントすることもできます。

> **ディレクションのコツ** : 指示は **1回につき1〜2個** に絞りましょう。一度に大量の修正を頼むよりも、細かくキャッチボールをした方がエージェントも正確に作業を進められます。

エージェントが変更を完了したら、ブラウザで再度確認して、次の修正を依頼する…というサイクルを繰り返してアプリを育てていきましょう。

### コード変更のレビュー

エージェントが変更したコードは **Code diffs** として表示されます。

- **Accept all** : すべての変更を受け入れる
- **Reject all** : すべての変更を拒否する
- **Review changes** : 詳細を確認してコメントする

気に入らない変更があれば、チャットで **↩️ Undo changes up to this point** を選択して元に戻すこともできます。


## ステップ 4 : デプロイしよう

アプリが完成したら、Web 上に公開（デプロイ）してみましょう。

### プロジェクト ID を確認する

デプロイ先の Google Cloud プロジェクト ID を確認します。Google Cloud コンソール ( https://console.cloud.google.com/ ) のダッシュボードを開き、「GDGSapporoAntigravityWorkshop」プロジェクトが表示されていることを確認します。別のプロジェクトが開かれている場合はヘッダーから変更できます。

**プロジェクト ID** の横のコピーボタンを押します。

![プロジェクト ID の確認](images/image40.png)

> **Note** : プロジェクト ID はプロジェクト名とは異なる場合があります。例えばプロジェクト名が「GDGSapporoAntigravityWorkshop」でも、プロジェクト ID は「gdgsapporoantigravity-12345」のような別の値になっていることがあります。

### エージェントにデプロイを依頼する

Agent Manager ウィンドウで Start new conversation をクリックし、**新しい会話を開始** します。会話の対象のワークスペースが正しいか確認します。

デプロイは Dockerfile の作成や Cloud Run の設定など複雑なタスクになるため、**Plan** を有効にして、モデルは **Gemini 3.1 Pro (High)** に戻しましょう。


事前にセットアップした Google Cloud プロジェクトの ID を伝えて、デプロイに必要なファイルの作成を依頼しましょう。デプロイ自体は Cloud Shell で行うため、ローカルに gcloud CLI をインストールする必要はありません。

```
このアプリを Google Cloud Run にデプロイして公開したいです。
Google Cloud のプロジェクト ID は「<上でコピーしたプロジェクトID>」です。
ローカルに gcloud CLI はインストールされていないので、デプロイに必要なファイル（Dockerfile など）を作成した上で、Google Cloud Shell で実行するデプロイ手順を教えてください。
```

![デプロイ計画の確認](images/image41.png)

> **Tip** : アプリ内で Gemini API を使いたい場合も、同じ Google Cloud プロジェクトで API を有効化して利用できます。

エージェントが Dockerfile の作成や Cloud Run の設定などのデプロイ計画を立ててくれます。内容を確認して、問題なければ **Proceed** をクリックしましょう。

![デプロイ計画の確認](images/image42.png)

作業が完了すると Walkthrough が作られるので確認します。

![Walkthrough の確認](images/image43.png)

Agent Manager ウィンドウでは、右のパネルで Artifact の一覧や変更ファイルの一覧が確認できます。例えば右のパネルの Dockerfile をクリックすると、Dockerfile の中身を確認できます。

![成果物の確認](images/image44.png)

### Cloud Shell でデプロイする

> **Note** : gcloud CLI がインストール済みの方は、Cloud Shell を使わずに Antigravity のターミナルからそのまま `gcloud run deploy` を実行できます。以下の手順はスキップして構いません。

エージェントが作成したファイルを使って、Cloud Shell からデプロイします。

1. Antigravity の Editor ウィンドウのターミナルで、プロジェクトフォルダを zip にします

```
zip -r ../my-app.zip . -x "node_modules/*" ".git/*" "my-app.zip" && mv ../my-app.zip .
```

> **Note（Windows の場合）** : Windows には `zip` コマンドがないため、代わりに PowerShell で以下を実行してください。
>
> ```powershell
> Get-ChildItem -Exclude node_modules, .git, my-app.zip | Compress-Archive -DestinationPath my-app.zip -Force
> ```

![zip ファイルの作成](images/image45.png)

2. Google Cloud コンソール ( https://console.cloud.google.com/ ) の右上にある **Cloud Shell をアクティブにする** ボタン（ターミナルアイコン）をクリックして、Cloud Shell を開きます

![Cloud Shell をアクティブにする](images/image46.png)

3. Cloud Shell のメニューバーにある **⋮**（その他）から **アップロード** を選択し、先ほど作成した zip ファイルをアップロードします

![Cloud Shell にアップロード](images/image47.png)

**ファイル** を選択し、**ファイル選択** ボタンから `my-app.zip` を選んで **アップロード** をクリックします。宛先ディレクトリはデフォルトのままで OK です。

![ファイルのアップロード](images/image48.png)

4. Cloud Shell で以下のコマンドを実行して、Cloud Run へのデプロイに必要な権限を設定します（新しいプロジェクトでは Cloud Build のサービスアカウントに必要なロールが付与されていないため、この手順が必要です）

```
gcloud services enable compute.googleapis.com cloudbuild.googleapis.com run.googleapis.com
```

```
PROJECT_NUMBER=$(gcloud projects describe $(gcloud config get-value project) --format='value(projectNumber)')
gcloud projects add-iam-policy-binding $(gcloud config get-value project) \
  --member="serviceAccount:${PROJECT_NUMBER}-compute@developer.gserviceaccount.com" \
  --role="roles/cloudbuild.builds.builder"
```

5. zip を展開してデプロイします

```
cd ~ && rm -rf my-app && unzip my-app.zip -d my-app && cd my-app
gcloud run deploy my-app --source . --region asia-northeast1 --allow-unauthenticated
```

> **Note** : Cloud Shell は Google Cloud コンソールで開いているプロジェクトが自動的に設定されるため、`--project` オプションは不要です。もしプロジェクトが異なる場合は `gcloud config set project <プロジェクトID>` で切り替えてください。

コマンドを実行すると、API の有効化について質問されます。

- **Do you want to enable these APIs to continue (Y/n)?** — `Y` を入力して Enter を押します（必要な API が自動で有効化されます）

デプロイには数分かかります。完了すると、公開 URL が表示されます。ブラウザで開いてアプリが動作していることを確認しましょう！

> **Tip** : デプロイが失敗した場合は、`Building Container... Logs are available at` の後に表示される URL をクリックすると、Cloud Console でビルドログを確認できます。エラーログを Antigravity のチャットに貼り付けて修正を依頼しましょう。
>
> ```
> Cloud Run にデプロイしようとしたら失敗しました。原因を調べて修正してください。
>
> <ビルドログをここに貼り付ける>
> ```
>
> 依存関係の競合や設定ミスなど、エージェントが原因を特定して修正してくれます。修正後は**再度 zip をアップロード**してデプロイし直しましょう。

> **Tip** : ここでは Cloud Run を使いましたが、「Firebase Hosting にデプロイして」「Vercel にデプロイして」のように好きなデプロイ先を指定すれば、エージェントがそれに合わせた手順で進めてくれます。


## クリーンアップ

ハンズオンで作成したリソースを削除して、不要な課金を防ぎましょう。

### Cloud Run サービスの削除

Cloud Shell で以下のコマンドを実行します。

```
gcloud run services delete my-app --region asia-northeast1
```

確認メッセージが表示されたら `Y` を入力して Enter を押します。

### プロジェクトの削除（任意）

プロジェクトごと削除すると、プロジェクト内のすべてのリソースがまとめて削除されます。

1. Google Cloud コンソールで **[IAM と管理]** > **[リソースの管理]** を開きます
2. ハンズオンで作成したプロジェクトを選択し、**[削除]** をクリックします
3. プロジェクト ID を入力して確認します

> **Note** : プロジェクトの削除は 30 日間の猶予期間があり、その間は復元可能です。


## クォータ節約＆開発のコツ

Antigravity のエージェント機能は非常に強力ですが、複雑な処理を丸投げしすぎると[レートリミット](antigravity-guide.md#レートリミットとクォータ)に達してしまうことがあります。以下のポイントを意識すると、クォータを節約しながら効率よく開発を進められます。

### 見た目の確認は人間の目でやる

エージェントに「プレビュー画面を見てデザインを確認して」と指示すると、画像の解析処理にクォータを消費します。プレビュー画面は **自分の目で確認して、「ボタンが右に寄りすぎている」のように言葉で指示** しましょう。

### エラーログは人間がコピペして渡す

「ボタンが動かないから調べて」と丸投げすると、エージェントはエラーの発生場所を探すためにログを遡り、余分なクォータを消費します。ターミナルやブラウザで出た **エラー文は、自分でコピーしてチャット欄に直接貼り付けて** 修正を依頼しましょう。

### ブラウザ検証を省略する

コードを生成させる際、エージェントが裏側でブラウザ検証を走らせることがあります。クォータを節約したい場合は **「ブラウザでの検証プレビューは実行しないでください」** と指示に添えましょう。

### 「Failed to send」と表示されたら

チャットで「Failed to send」と表示されてメッセージが送れない場合は、一度 Antigravity からログアウトして、再度ログインしてみてください。


## ステップ 5 : さらにカスタマイズしよう（時間がある方向け）

時間がある方は、以下のようなことにも挑戦してみましょう。

### ルールを追加する

[ルール](antigravity-guide.md#ルール)を追加して、エージェントの動作をカスタマイズできます。例えば「日本語でコメントを書いて」「和風デザインにして」など。

### ワークフローを活用する

よく使うプロンプトを[ワークフロー](antigravity-guide.md#ワークフロー)として保存し、`/` で呼び出すことができます。

### ブラウザサブエージェントを使う

Antigravity の[ブラウザ機能](antigravity-guide.md#ブラウザ)を使うと、エージェントが Web ページを閲覧して情報を収集できます。

```
札幌の桜の名所について、Web で情報を調べて、
アプリに追加するデータを作成してください。
```

### インラインコマンドを使う

[エディタ](antigravity-guide.md#エディタ)で `Cmd + I`（Mac）/ `Ctrl + I`（Windows）を押すと、自然言語でインライン補完をリクエストできます。ちょっとした修正に便利です。


## 今日体験したこと

- **AIとの壁打ちによるアイデアの具現化（要件定義）** : ぼんやりしたアイデアをAIにぶつけ、対話を通じて具体的な機能要件へと落とし込みました
- **自律型エージェントへのタスク委譲** : 環境構築、UIコンポーネントの作成、ロジックの実装といった複雑なタスクをAntigravityに「任せる」体験をしました
- **ゼロからデプロイまでの一気通貫プロトタイピング** : AIが生成したコードをプレビューで確認・修正しながら作り上げ、Web上にデプロイするところまでを体験しました


## 参考資料・コンテンツ

- [Antigravity ガイド](antigravity-guide.md) : Antigravity の機能や設定についての詳細
- [参考リンク集](antigravity-guide.md#参考資料コンテンツ) : 公式サイト、ドキュメント、Codelab など
