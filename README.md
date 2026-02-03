# sqrdots.dctl

Block平均（モザイク） + 輝度/彩度の段階量子化 + 4x4 Bayerディザ（β版 2026-01-30）

## 特徴
- Blockごとに平均色（モザイク化）
- Y（輝度）を段階量子化 + 4x4 Bayerディザ
- C（色成分）の大きさ（彩度）を段階量子化 + 4x4 Bayerディザ  
  - 色相は保ち、彩度量のみディザで揺らします
- 彩度スケール、元画像とのブレンド調整

## 動作要件
- DaVinci Resolve（DCTL対応版）
- 期待入力：0〜1レンジのRGB（タイムライン/ノード構成に依存）

## インストール
### Windows
`sqrdots.dctl` を次へ配置：
`C:\ProgramData\Blackmagic Design\DaVinci Resolve\Support\LUT\DCTL\`

その後、Resolveを再起動（またはLUT/DCTL一覧を更新）。

## 使い方
- ColorページでDCTLとして `sqrdots.dctl` を適用してください。
- ブロック平均は計算量が増えます。高解像度・大きいBlock_Sizeで重い場合があります。

## パラメータ
- `Block_Size`：ブロックサイズ（px）
- `Luma_Tone_Levels`：輝度の段数（2〜8）
- `Luma_Dither_Str`：輝度ディザ強度（0でOFF）
- `Chroma_Tone_Levels`：彩度の段数（2〜8）
- `Chroma_Dither_Str`：彩度ディザ強度
- `Chroma_Strength`：全体彩度スケール（0でモノクロ寄り）
- `Blend`：元画像とのブレンド

## 注意
- 出力は0〜1にクリップします。
- 彩度量の正規化は `satN = clip01(|C|)` を採用しています（強彩度領域は飽和します）。

## License
MIT License（`LICENSE` を参照）
