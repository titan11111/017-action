# LEARNINGS — 017-action

## 2026-08-03 — 404調査 / nextStage 二重ループ

- 公開URL `https://titan11111.github.io/017-action/` と必須アセット（hero/enemy*/maou/BGM）はすべて HTTP 200。参照切れの静的404は再現せず。
- 旧参照 `image_0.png` / `script.js` / `style.css` は今も単体URLだと404だが、現行 `index.html` からは読んでいない。キャッシュで古いHTMLが残ると画像404に見える。
- `nextStage()` で素の `gameLoop()` を足すと RAF が二重化し、クリア後の移動速度が約2倍になる（実測 ratio 2.00）。`restartGameLoop()` で cancel→1本再起動に統一。
- BGMパスは `encodeURI`、画像は `?v=` でキャッシュずれを避ける。

## 2026-08-03 — ステージ別背景

- 黒残像塗り（`rgba(0,0,0,0.1)`）が画面を暗くしていたため廃止。毎フレーム `drawStageBackground` で全面再描画。
- 基調は中明度グラデ。装飾は低不透明度（〜0.18）で足場・敵を邪魔しない。
- motif: grid / city / stream / matrix / core / void / nexus / quantum / storm / boss。

## 2026-08-03 — iOS UI / タッチ / 音声 / 打感

- 画面下25%を `#fcPad`（ファミコン風十字＋Aジャンプ）に固定。上75%が `#gameStage`。
- ダブルタップズーム防止（touchend 300ms）、選択・長押し・ドラッグ禁止を追加。
- iOS音声: `unlock` + `ensureResumed` + `visibilitychange`/`pageshow`/`focus` で復帰再開。STARTジェスチャ内で `init`→`unlock`→`playBGM`。
- 打感: `pointerdown` + `setPointerCapture` + `is-pressed` + `vibrate(15)` + WebAudio「カチッ」。
- harness の `button.first()` 対策で START を DOM 先頭側へ配置。
