# コード聴音トレーニングアプリ（開発メモ・AI向け引き継ぎ）

どのAI（Claude Code / Codex / Cursor / Gemini など）でも、まずこのファイルを読んでから作業すること。

## 概要
- 耳でコード（和音）を聞き取れるようになるための練習アプリ
- `ultimate-complete-app.html` 1ファイルで完結（HTML/CSS/JS込み、外部ライブラリなし、Vanilla JS）
- ブラウザでダブルクリックして開けば動く（file:// で動作すること）
- スマホ（特にiPhone Safari）でも使えることが必須
- 音：Web Audio API（Oscillator + Gain）で合成／読み上げ：speechSynthesis（英語）

## 主な機能（現状）
- タブ：単音コード／コード進行／聴音訓練／高度な設定／練習統計
- キー12個・コードタイプ16種（Major, Minor, Dom7, Maj7, Min7, Dim, Aug, Sus4, 6th, 9th, 11th, 13th, Add9, Maj9, Min9, Dim7）を複数選択
- コード名・構成音の読み上げ（コード前/後）、アルペジオ、ルート強調、転調、繰り返し回数
- コード進行15パターン、スケール練習、メトロノーム
- 聴音訓練：再生→選択肢から回答
- ライト/ダーク切替、日本語/English切替、ログ表示

## 経緯
- 2026/3/8版：`~/chord-training-app/ultimate-complete-app.html`（バックアップ。仕様書 PROMPT_FOR_OTHER_AI.md もそこにある）
- 2026/3/9版（このフォルダ・最新）：iPhoneで音/読み上げが出ない問題対策として、音声有効化とTTS処理を「awaitで待たない同期処理」に変更。TTSが終わらない場合は7秒で強制リセット
- iPhone実機で直ったかは未確認

## 既知の問題
- （解決済み 2026/10/30）画面下の固定表示がコンテンツに重なる問題 → bodyに下余白を追加、スマホ幅ではステータスをボタンの上の段に移動

## 作業ルール
- 1ファイル構成を維持する（分割しない）
- iPhone対策：音・読み上げの開始はユーザーのタップの処理内で同期的に呼ぶ（間にawait/setTimeoutを挟まない）
- 変更したらgitでコミットしてから次へ（リモート：github.com/RYUICHI4568/Code-Listening-Training-Part-1）
- 回答・UI文言は日本語
