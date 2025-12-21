---
name: studiojinsei-nanobanana
description: StudioJinsei用Nanobanana画像生成Skill。Google Gemini APIを使用してロゴ、コトネちゃん、サイトビジュアル等を生成します。
allowed-tools:
  - bash
  - read
  - write
  - glob
---

# StudioJinsei Nanobanana 画像生成 Skill

## 概要

StudioJinseiのブランドビジュアルを生成するためのNanobanana Skillです。
Google Gemini APIを直接使用して、ロゴ、コトネちゃん、サイトビジュアル等を生成します。

---

## 📋 利用モデル

| モデル名 | API名 | 特徴 | 料金目安 |
|---------|-------|------|----------|
| **Gemini 3 Pro Image** | gemini-3-pro-image-preview | 高品質・高解像度 | 約21-30円/枚 |
| Gemini 2.5 Flash Image | gemini-2.5-flash-image | 高速・低コスト | 約6円/枚 |

**推奨：** StudioJinseiのロゴやメインビジュアルは **Gemini 3 Pro Image** を使用

---

## 🔧 前提条件

### 必須
- Google API Key（`GOOGLE_API_KEY`）
- Python 3.x
- google-generativeai パッケージ

### 環境変数
```bash
export GOOGLE_API_KEY="AIzaSyBs2FQS6FYWwx9LKQdyywkBFTEXt5tK9Z8"
```

---

## ⚙️ セットアップ手順

### 1. 環境変数を設定

#### macOS/Linux（zsh）の場合
```bash
# ~/.zshrc を編集
nano ~/.zshrc

# 以下を追加
export GOOGLE_API_KEY="AIzaSyBs2FQS6FYWwx9LKQdyywkBFTEXt5tK9Z8"

# 設定を反映
source ~/.zshrc

# 確認
echo $GOOGLE_API_KEY
```

### 2. Python パッケージをインストール

```bash
pip install google-generativeai
```

---

## 🚀 基本的な使い方

### 画像生成スクリプト（簡易版）

```python
import google.generativeai as genai
import os
from pathlib import Path

# API設定
genai.configure(api_key=os.environ["GOOGLE_API_KEY"])

# モデル選択
model = genai.GenerativeModel("gemini-3-pro-image-preview")  # または "gemini-2.5-flash-image"

# プロンプト
prompt = """
[ここにプロンプトを記述]
"""

# 画像生成
response = model.generate_content(prompt)

# 保存
output_path = Path("images/studiojinsei/output.png")
output_path.parent.mkdir(parents=True, exist_ok=True)

if response.candidates and response.candidates[0].content.parts:
    image_data = response.candidates[0].content.parts[0].inline_data.data
    output_path.write_bytes(image_data)
    print(f"画像を保存しました: {output_path}")
```

---

## 📝 プロンプトの作り方

### 基本テンプレート

すべてのプロンプトに以下を含める：

```
[StudioJinsei Brand Foundation]

Concept: "Making invisible thoughts visible and tangible"
Tagline: "考えが動きに変わるきっかけをつくるスタジオ"

Visual direction:
- Simple yet warm (not cold)
- Organized yet approachable (not rigid)
- Sophisticated yet friendly (not intimidating)
- Professional yet personal (not distant)

Color palette: Soft mint green (#A8D5BA), dark teal (#1D4E4A), pale mint (#E8F5EE), white (#FFFFFF).
Main: soft mint green (#A8D5BA), accent: dark teal (#1D4E4A).

Typography: Modern sans-serif, Poppins or similar clean font style.

Design style:
- Minimalist, Apple-inspired clean aesthetic
- Plenty of white space, generous breathing room
- Simple, uncluttered, focused layout
- High quality, attention to detail

Avoid:
- Flashy, overly colorful, hyper-energetic styles
- Spiritual, abstract, mystical vibes
- Cold, corporate, distant aesthetics
- Cheap, low-quality appearance

---

[ここに具体的な指示]
```

---

## 🎯 生成パターン

### パターン1：ロゴ生成

**プロンプト例：**
```
[StudioJinsei Brand Foundation]
...

Professional wordmark logo for "StudioJinsei".
Text-only design, no symbols or icons.
Typography: Modern sans-serif, Poppins or similar clean font.
"Studio" in light/thin weight, "Jinsei" in medium/semibold weight.
Color scheme: Dark teal (#1D4E4A) for main text, soft mint green (#A8D5BA) subtle accent.
Minimalist, sophisticated, professional yet approachable.
Clean letterforms with generous letter spacing.
Plenty of white space around the text.
High quality vector style.
```

**参照：** [brand-foundation.md](./brand-foundation.md)

### パターン2：コトネちゃん生成

**プロンプト例：**
```
[StudioJinsei Brand Foundation]
...

A soft, hand-drawn style illustration of Kotone-chan.
Young Japanese woman with dark long hair.
Mint green bucket hat with subtle leaf pattern.
White elegant clothing.
Gentle, warm illustration style with soft lines.
Muted, sophisticated color palette (soft mint #A8D5BA, dark teal #1D4E4A).
Calm, professional, trustworthy expression with a gentle smile.
Minimal background, plenty of white space.
Apple-inspired clean aesthetic.
She embodies "making invisible thoughts visible" concept.
```

**参照：** [kotone-character.md](./kotone-character.md)

### パターン3：サイトビジュアル生成

**プロンプト例：**
```
[StudioJinsei Brand Foundation]
...

Website hero section design for StudioJinsei.
Main headline: "考えが動きに変わるきっかけをつくるスタジオ"
Subheadline: "見えない思いを、見える形に"
Background: Soft mint green gradient (#E8F5EE to #FFFFFF).
Minimalist hand-drawn style illustration of Kotone-chan (optional).
Plenty of breathing room, clean and uncluttered.
Professional yet friendly, modern and sophisticated.
```

---

## 📐 解像度設定

Gemini APIでは解像度を直接指定できませんが、プロンプトで要求できます：

```
Generate a 1024x1024 square image.
High resolution, suitable for professional use.
```

または

```
Generate a 1920x1080 (16:9) landscape image.
```

---

## 💰 料金目安

### API料金
| 解像度相当 | 1枚あたりの料金 |
|----------|----------------|
| 1K (1024x1024) | 約21円 |
| 2K (2048x2048) | 約42円 |
| 4K (4096x4096) | 約85円 |

### 制作例
**ロゴ制作：**
- 3パターン生成 = 約63円
- 最終版高解像度 = 約85円
- **合計：約150円**

---

## 📋 チェックリスト

生成時に必ず確認：

- [ ] [brand-foundation.md](./brand-foundation.md) を参照したか
- [ ] カラーパレット（#A8D5BA, #1D4E4A）が正しいか
- [ ] 「シンプル、でも冷たくない」が表現されているか
- [ ] 余白がたっぷりあるか
- [ ] StudioJinseiの核心コンセプトが伝わるか
- [ ] NGデザイン（キラキラ、スピリチュアル、冷たい、チープ）になっていないか

---

## 🖼️ 参照画像

### 画像の場所

このディレクトリ（`nanobanana-base`）には参照画像が含まれています：

```
nanobanana-base/
└── images/
    └── reference/
        ├── line-profile.jpg        # LINEプロフィール画像
        └── officialprofile.PNG     # 公式プロフィール画像
```

### Claudeスキルでの使用

新しいリポジトリでClaudeスキル（`.claude/skills/kotone-*`）を使用する場合：

1. **スキルディレクトリに画像をコピー**
   ```bash
   mkdir -p .claude/skills/kotone-business/images
   cp docs/nanobanana-base/images/reference/* .claude/skills/kotone-business/images/
   ```

2. **SKILL.mdで参照**
   ```markdown
   ## 参照画像
   
   | 用途 | パス |
   |------|------|
   | LINEプロフィール画像 | `images/line-profile.jpg` |
   | 公式プロフィール画像 | `images/officialprofile.PNG` |
   ```

詳細は [setup-guide.md](./setup-guide.md) の「Claudeスキルに参照画像を配置」セクションを参照してください。

---

## 🔗 関連資料

- [ブランド共通デザイン土台](./brand-foundation.md)
- [コトネちゃん設定](./kotone-character.md)
- [セットアップガイド](./setup-guide.md)
- [使い方ガイド](./usage-guide.md)
- [README](./README.md)

---

## 🎓 Tips

### プロンプト作成のコツ
1. 必ず共通プロンプト基盤を含める
2. カラーコードを明記（#A8D5BA, #1D4E4A）
3. 避けるべきものを明記（Avoid:）
4. 具体的に、曖昧な表現を避ける

### 品質管理
1. 生成後は必ずチェックリスト確認
2. プロンプトを保存してバージョン管理
3. 複数パターン生成して比較

---

**最終更新：2025/12/20**
