---
name: nanobana-comic-creator
description: NanobananaProを使用して画像を生成するSkill。slomap-note-automationリポジトリのnanobanana.pyスクリプトを呼び出し、Markdownプロンプトから画像生成を行います。4コマ漫画、キャラクター画像、ロゴ生成に使用してください。
allowed-tools:
  - bash
  - read
  - write
  - glob
---

# NanobananaPro 画像生成 Skill

## 概要
slomap-note-automationリポジトリの`scripts/nanobanana.py`を使用して画像を生成します。

## 利用モデル
| モデル名 | API名 | 特徴 |
|---------|-------|------|
| nano_banana_pro | gemini-3-pro-image-preview | 高品質・高解像度 |
| nano_banana | gemini-2.5-flash-image | 高速・低コスト |

## 前提条件
- 環境変数 `GOOGLE_API_KEY` が設定されていること
- 環境変数 `NANOBANANA_REPO_PATH` でリポジトリパスを指定（デフォルト: `~/Desktop/slomap-note-automation`）

## セットアップ（別PC用）

```bash
# 1. slomap-note-automationリポジトリをクローン
git clone https://github.com/dataanalytics2020/slomap-note-automation.git ~/Desktop/slomap-note-automation

# 2. 環境変数を設定（~/.zshrc または ~/.bashrc に追加）
export GOOGLE_API_KEY="your-google-api-key"
export NANOBANANA_REPO_PATH="$HOME/Desktop/slomap-note-automation"

# 3. 依存関係をインストール
cd ~/Desktop/slomap-note-automation
pip install -r requirements.txt
```

## 基本コマンド

**⚠️ 重要: 常に `-r 1k` を指定すること（コスト最適化）**

```bash
# リポジトリパスを環境変数から取得（デフォルト: ~/Desktop/slomap-note-automation）
REPO_PATH="${NANOBANANA_REPO_PATH:-$HOME/Desktop/slomap-note-automation}"
cd "$REPO_PATH"

# 基本実行（1k解像度を必ず指定）
python scripts/nanobanana.py prompts/my_prompt.md -r 1k

# 参照画像付き（絵柄統一に使用）
python scripts/nanobanana.py prompts/my_prompt.md -r 1k -i "images/reference.png"

# 複数参照画像
python scripts/nanobanana.py prompts/my_prompt.md -r 1k -i "image1.png" -i "image2.png"

# フラット出力（サブフォルダなし）
python scripts/nanobanana.py prompts/my_prompt.md -r 1k --output-dir images/slomap --flat

# ドライラン（プロンプト確認のみ）
python scripts/nanobanana.py prompts/my_prompt.md -r 1k --dry-run
```

## オプション一覧

| オプション | 説明 |
|-----------|------|
| `-n, --name` | 出力ファイル名 |
| `-r, --resolution` | 解像度 (square, 1k, 2k, 16:9, 9:16, fhd, hd) |
| `-o, --output-dir` | 出力ディレクトリ |
| `-i, --image` | 参照画像パス（複数指定可、最大14枚） |
| `--flat` | フォルダを作らず直接出力 |
| `--dry-run` | プロンプト確認のみ |

## 解像度設定

| キー | サイズ | 用途 | 料金 |
|------|--------|------|------|
| **1k** | 1024x1024 | **推奨（デフォルト）** | 約21円 |
| 2k | 2048x2048 | 高解像度正方形 | 約42円 |
| 4k | 4096x4096 | 超高解像度 | 約85円 |
| hd | 1280x720 | YouTube HD | - |
| fhd | 1920x1080 | YouTube FHD | - |
| 16:9 | 1536x864 | 一般的な横長 | - |
| 9:16 | 864x1536 | 縦長（4コマ漫画） | - |

**💰 コスト最適化**: 基本は `1k` を使用。高解像度が必要な場合のみ `2k` 以上を検討。

## プロンプトファイル形式

```markdown
# タイトル（任意）

## 設定
- resolution: 16:9
- name: my_image

## 参照画像（任意）
- images/reference.png

## プロンプト
ここに画像生成プロンプトを書く...
```

## スロマップAI用キャラクター

### 🐱 ネコ「サガすちゃん」（ユーザー代表）
- 好奇心旺盛、元気、ちょっとドジ
- 水色パーカー、スマホ、リュック
- 使用場面: 検索UI、チュートリアル、Empty State

### 🐻 クマ「ガイドくん」（AI/ガイド担当）
- 落ち着いている、優しい、包容力
- 紺カーディガン、白シャツ
- 使用場面: AI機能説明、オンボーディング、ヘルプ

### 🐰 ウサギ「ミミちゃん」（情報収集担当）
- 好奇心旺盛、素早い、おっちょこちょい
- ピンクワンピース、ヘッドホン、メモ帳
- 使用場面: 通知、取材情報、ニュース

## 4コマ漫画生成手順

1. GitHub Issue確認（slomap-note-automationリポジトリ）
2. 各フレームのプロンプトファイルを作成
3. 参照画像（既存キャラ画像）を指定して生成
4. 生成結果をIssueにコメント

## API料金目安

| 解像度 | 1枚あたりの料金 |
|--------|----------------|
| 1K (1024x1024) | 約21円 |
| 2K (2048x2048) | 約42円 |
| 4K (4096x4096) | 約85円 |

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

## 関連リンク
- [slomap-note-automation リポジトリ](https://github.com/dataanalytics2020/slomap-note-automation)
- [Nano Banana Pro 参考記事](https://note.com/yuichirohonda/n/nf92bf6f3e292)
