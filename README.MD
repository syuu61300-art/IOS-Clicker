# Clicker（iPhone用 Webアプリ）

iPhoneのSafariで「ホーム画面に追加」すると、アプリのように全画面で使えるオートクリッカーです。

## 機能
- **クリック位置**：「中央」（ボタンの中心）か「指定場所」（タップ／ドラッグで決めた位置）を選択
- **フレームレート連動の速度**：画面の更新（requestAnimationFrame）ごとにクリック
  - 速度 = fps ×「1フレームあたりのクリック数」÷「何フレームごと」
  - 例：60fps・1回・1フレームごと → 60回/秒、120fps・2回 → 240回/秒、60fps・1回・6フレームごと → 10回/秒
- 実測fps・実測CPSを表示、カウントと設定は自動保存
- **閉じても止まらない**：アプリを閉じても（スワイプで終了しても）実行状態を保持し、戻ったときに閉じていた間のクリック数を加算。止まるのは「停止」を1秒長押ししたときだけ
- **誤作動防止**：停止は1秒・リセットは0.8秒の長押しが必要／実行中は設定をロック／実行中の手のタップは数えない／一瞬のアプリ切替や時計の異常値は無視
- 実行中は画面を点灯したまま（iOS 16.4以降）、オフラインでも起動

## GitHub Pagesで公開する
1. GitHubで新しいリポジトリ（例：`ios-clicker`、Public）を作る
2. このフォルダのファイルをすべてアップロード（`index.html` がリポジトリ直下に来るように）
   - ブラウザなら「Add file › Upload files」でフォルダの中身をドラッグ
   - コマンドなら：
     ```sh
     git init && git add . && git commit -m "Clicker"
     git branch -M main
     git remote add origin https://github.com/<ユーザー名>/ios-clicker.git
     git push -u origin main
     ```
3. リポジトリの **Settings › Pages** で Source を「Deploy from a branch」、Branch を `main` / `/(root)` にして Save
4. 1〜2分後に `https://<ユーザー名>.github.io/ios-clicker/` で開けます

## iPhoneでアプリ化する
1. SafariでそのURLを開く
2. 共有ボタン › **ホーム画面に追加**（「Webアプリとして開く」をオン）
3. ホーム画面のアイコンから起動

## 120fpsで動かす（ProMotion搭載機種）
iOSのSafariは標準で60fpsに制限されています。
設定 › アプリ › Safari › 詳細 › 機能フラグ › **Prefer Page Rendering Updates near 60fps** をオフにすると120fpsになります。
アプリ内の「実測fps」で確認できます。低電力モード中は60fps以下になることがあります。

## 注意
Webアプリの制限により、クリックできるのは **このアプリの画面内だけ** です。
iOSは閉じたWebアプリのプログラムを一時停止するため、閉じている間のクリックは「経過時間 × 速度」で計算して戻ったときに加算します。
「指定場所」がボタンから外れている場合は加算しません。
他のアプリやゲームをタップすることはできません。
