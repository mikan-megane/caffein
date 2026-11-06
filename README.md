# Caffein

iPhone の PiP (ピクチャー・イン・ピクチャー) を利用してスリープを防止する、1 ファイルの Web アプリです。

GitHub Pages: <https://mikan-megane.github.io/caffein/>

## 仕組み

iPhone では PiP 起動中は画面が消えにくくなる性質を利用し、無音の動画を常時再生することでスリープを防止します。

- 動画はあえて **480×16 (30:1) の超横長** にしてあります。PiP ウィンドウは動画のアスペクト比に追従するため、PiP が細い横長バーとして小さく表示されます(1:1 だと大きすぎるため)
- システムのカラースキームに追従
  - ダークモード → 黒い動画 (`silent-dark.mp4`)
  - ライトモード → 白い動画 (`silent-light.mp4`)

## 機能

- **Start / Stop PiP** — 再生の開始・停止
- **スリープタイマー** — 5 / 15 / 30 / 60 分のプリセットまたは任意分数を指定。カウントダウン後に PiP と動画を自動停止

## 使い方

iPhone (Safari) でページを開き、**Start PiP** をタップするだけです。

## ファイル構成

| ファイル | 役割 |
|---|---|
| `index.html` | アプリ本体 (HTML / CSS / JS すべて込み) |
| `silent-dark.mp4` | ダークモード用の黒い無音動画 |
| `silent-light.mp4` | ライトモード用の白い無音動画 |
| `silent.mp4` | 旧バージョン用の正方形動画 (未使用) |

## 開発

ビルド・依存パッケージなし。`index.html` を編集するだけで完了です。

動画を差し替える場合は ffmpeg で生成できます:

```
ffmpeg -f lavfi -i color=c=black:s=480x16:r=25 -t 5 \
  -c:v libx264 -pix_fmt yuv420p -movflags +faststart silent-dark.mp4
```
