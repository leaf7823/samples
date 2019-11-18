
## [Wait Queue Item (キュー アイテムを待つ)] アクティビティのサンプルワークフロー

### Description
UiPath 19.4 でリリースされた [キュー アイテムを待つ (Wait Queue Item)] アクティビティのサンプル ワークフローのご紹介です。
[キュー アイテムを待つ (Wait Queue Item)] アクティビティは、指定されたキューにアイテムを取りに行き、キュー アイテムが見つかればそれを QueueItem 型の変数に格納します。キュー アイテムの取得後は、キュー アイテムのステータスが [新規 (New)] から [実行中 (In Progress)] に変わります。 
[キュー アイテムを待つ (Wait Queue Item)] アクティビティは、[トランザクション アイテムを取得 (Get Transaction Item)] アクティビティと異なり、アクティビティ実行時に指定されたキューが空だった場合、そのキューに新しいキュー アイテムが追加されるまで待機します。
本サンプルでは、次の 2 種類のワークフロー プロジェクトを作成しました。

- **WaitQueueItemProducer**: キューにトランザクション データを追加するワークフロー
- **WaitQueueItemConsumer**: WaitQueueItemProducer ワークフローによって追加されたキュー アイテムを取得し、デモ アプリにデータを投入するワークフロー

**WaitQueueItemProducer** ワークフローは、事前に用意された Excel ファイルのデータを読み込み、そのデータを [キュー アイテムを追加 (Add Queue Item)] アクティビティを使用し 1 件ずつキューに追加します。**WaitQueueItemConsumer** ワークフローは、[キュー アイテムを待つ (Wait Queue Item)] アクティビティを使用し、指定されたキューにキュー アイテムを取得しに行きます。新しいキュー アイテムが存在しなければタイムアウトするまで待機します。キュー アイテムを取得することができた場合、キュー アイテムの固有データを、あらかじめ立ち上げておいたデモ アプリに [文字を入力 (Type Into)] アクティビティを使用して入力します。デモ アプリの [実行] ボタンを押してデータの登録を行った後、再び [キュー アイテムを待つ (Wait Queue Item)] アクティビティを使用して新しいキュー アイテムを待ちます。

### Note
- このワークフローを実行するには、Orchestrator に接続している必要があります
- Orchestrator に SampleQueue という名前のキューを作成しておく必要があります
- デモ アプリ (UiPathデモアプリ_ログイン画面.exe) が、あらかじめデスクトップ上に存在している必要があります。デモ アプリは UiPath アカデミーの Orchestrator トレーニングからダウンロードできます
- サンプル ワークフローを簡素化するために、[パスワードを取得 (Get Password)] アクティビティが使用されています。このアクティビティは現在のユーザーに紐づけてパスワードを暗号化するため、ワークフローを実行する前にパスワードを入力し直してください。ログイン ユーザーとパスワードの情報はデモ アプリのログイン画面に記載されています
- WaitQueueItemProducer ワークフローは [Excel アプリケーション スコープ (Excel Application Scope)] アクティビティを使用して Excel ファイルを読み込むため、実行環境に Office がインストールされている必要があります

### References

- [[キュー アイテムを待つ (Wait Queue Item)] アクティビティガイド](https://docs.uipath.com/activities/lang-ja/docs/wait-queue-item)