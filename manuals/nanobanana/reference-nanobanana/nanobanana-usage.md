# Nano Banana Pro 詳細使用ガイド

## ファイル構成

```
slomap-note-automation/
├── scripts/
│   └── nanobanana.py          # メインスクリプト
├── src/
│   ├── api/
│   │   └── gemini_image_client.py  # Gemini API クライアント
│   └── content/
│       └── image_manager.py        # 画像管理クラス
├── prompts/                    # プロンプトファイル
└── images/                     # 生成画像
```

## プロンプトファイル例

### 基本形式
```markdown
# キャラクター生成プロンプト

## 設定
- resolution: 16:9
- name: my_character

## 参照画像
- images/reference/style_guide.png

## プロンプト
Generate a cute anime-style character...
```

### 4コマ漫画用プロンプト例
```markdown
# 4コマ漫画 - 来店動機編

## 設定
- resolution: 9:16
- name: comic_visit_motivation

## 参照画像
- images/lp/slogacha_char_shiba.png
- images/lp/slogacha_char_tanuki.png

## プロンプト
Create a 4-panel manga (yonkoma) style comic strip.
The comic should be vertically stacked with 4 equal-sized panels.

Panel 1: [Setup]
A cute Shiba Inu character looking at their smartphone with a curious expression.
The screen shows "スロガチャ開催中?" (Slot Gacha happening?)

Panel 2: [Development]
The Shiba Inu looking excited, imagining golden coins and stars.
Thought bubble: "行かなきゃ！" (I have to go!)

Panel 3: [Turn]
The Shiba Inu rushing to the pachinko parlor, motion lines showing speed.

Panel 4: [Conclusion]
The Shiba Inu happily at the parlor, with the Tanuki store manager welcoming them.
Text: "いらっしゃいませ！" (Welcome!)

Style: Cute, anime-style, colorful, game-like aesthetic with sparkle effects.
```

## API料金目安

| 解像度 | 1枚あたりの料金 |
|--------|----------------|
| 1K (1024x1024) | 約21円 |
| 2K (2048x2048) | 約42円 |
| 4K (4096x4096) | 約85円 |

※ Google AI Studio経由の場合

## トラブルシューティング

### GOOGLE_API_KEY エラー
```bash
# 環境変数を確認
echo $GOOGLE_API_KEY

# 設定されていない場合
export GOOGLE_API_KEY="your-api-key"
```

### 画像生成失敗
- プロンプトが長すぎる場合は短くする
- 参照画像が多すぎる場合は減らす（最大14枚）
- APIレート制限の場合は少し待つ

### 絵柄が安定しない
- 参照画像を必ず指定する（`-i` オプション）
- スタイル指定を詳細にプロンプトに含める
