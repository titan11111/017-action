# SPEC — 017-action（サイバーパンク・ネオシティ・アクション）

## ゲーム概要
10ステージの横スクロール風プラットフォームアクション。足場ギミック・敵回避・ゴール到達でクリア。

## 対象端末
- 主戦場: iPhone Safari（縦持ち）
- 配信: GitHub Pages（`https://titan11111.github.io/017-action/`）

## 画面 / 状態遷移
`menu` → `playing` → `stageClear` / `gameOver` / `gameComplete`

## 操作
- キーボード: ← → / Space・↑ ジャンプ
- モバイル: 下25% FCパッド（← → / A=JUMP）
- START タップで Audio unlock

## コアループ
足場を渡り敵を避けゴール（★）へ到達 → 次ステージ。ライフ0でゲームオーバー。

## 勝敗条件
- クリア: ステージ10クリア
- 敗北: ライフ0、または落下

## UI
- HUD: STAGE / LIFE / SCORE / BGM・SEトグル
- 下25%: ファミコン風コントローラー
- ステージ別中明度背景（装飾は低不透明度）

## 音声
- BGM: `audio/Neon Circuitry.mp3` / ボス `audio/tobu.mp3`
- SE: WebAudio（ジャンプ・取得・ヒット・打感カチッ）
- iOS: ジェスチャ内 unlock + 復帰時 resume

## 保存
なし（セッション完結）

## ファイル構成
- `index.html`（単一ファイル）
- `audio/` / 画像PNG（フォルダ直下）
- `SPEC.md` / `LEARNINGS.md`

## 実装制約
- iOS: viewport-fit / touch-action / ダブルタップ防止 / safe-area / Audio unlock
- 背景はプレイの視認性を優先（濃い黒ベタにしない）

## テスト項目
- [x] harness PASS（描画・タップ・コンソール0）
- [ ] iPhone実機の音・打感（未検証）

## 未確定事項
なし（公開ブロッカーなし）
