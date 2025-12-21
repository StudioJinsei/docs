# Nanobanana Base｜StudioJinsei

**作成日：2025/12/20**

StudioJinseiのすべてのビジュアル制作で共通して使用する基本セットです。
ロゴ、サイト、LINE、SNS等、どのビジュアルを作る時もこのディレクトリを参照してください。

---

## 📁 このディレクトリについて

### 目的
- StudioJinseiのブランドデザインを統一
- Nanobananaでの画像生成を効率化
- プロンプト作成の土台を提供

### 使い方
1. ビジュアルを作りたい時、このディレクトリを開く
2. 用途に応じて必要なファイルを参照
3. プロンプトを作成して、Nanobananaで生成

---

## 📂 ファイル構成

```
nanobanana-base/
├── README.md                    # このファイル
├── brand-foundation.md          # ブランド共通デザイン土台★
├── kotone-character.md          # コトネちゃん設定★
├── setup-guide.md               # Nanobananaセットアップ方法
├── usage-guide.md               # 画像生成ガイド
└── images/                      # 参照画像
    └── reference/               # コトネちゃんのプロフィール画像等
        ├── line-profile.jpg
        └── officialprofile.PNG
```

★ = すべてのビジュアル制作で必ず参照するファイル

---

## 🎯 各ファイルの役割

### 1. brand-foundation.md
**StudioJinseiのブランドデザイン共通土台**

含まれる内容：
- キャッチコピー、会社コンセプト
- ビジュアル方向性（シンプル、でも冷たくない等）
- カラーパレット（#A8D5BA, #1D4E4A等）
- タイポグラフィ（Poppins等）
- デザイン原則（Apple風ミニマル）
- Nanobanana用共通プロンプト基盤

**使い方：**
すべてのプロンプトに「[StudioJinsei Brand Foundation]」セクションとして含める

### 2. kotone-character.md
**コトネちゃん（代表キャラクター）の設定**

含まれる内容：
- 外見設定（ダークロングヘア、ミントグリーンのバケットハット等）
- 表情の原則（穏やかな微笑み、信頼感）
- Nanobanana用プロンプト（基本版、簡易版、全身版）
- 使用場面別ガイド

**使い方：**
コトネちゃんを含むビジュアルを作る時に参照

### 3. setup-guide.md
**Nanobananaのセットアップ方法**

含まれる内容：
- slomap-note-automationリポジトリのクローン方法
- 環境変数設定（GOOGLE_API_KEY等）
- 基本コマンド
- オプション一覧
- 解像度設定、料金目安

**使い方：**
初めてNanobananaを使う時、または環境を再構築する時に参照

### 4. usage-guide.md
**画像生成の使い方ガイド**

含まれる内容：
- プロンプトファイルの作り方
- ロゴ、コトネちゃん、サイトビジュアル等の生成例
- 実行コマンド例
- プロンプト作成のコツ
- 生成後のチェックリスト

**使い方：**
実際に画像を生成する時に参照

---

## 🚀 クイックスタート

### Step 1: セットアップ（初回のみ）

#### 1-1. StudioJinseiリポジトリ確認・クローン
```bash
cd ~/Desktop/StudioJinsei/docs/nanobanana-base
```

このディレクトリがあればOK！なければリポジトリをクローン：
```bash
cd ~/Desktop
git clone [StudioJinseiリポジトリURL] StudioJinsei
```

#### 1-2. 環境変数を設定
```bash
# ~/.zshrc を編集
nano ~/.zshrc

# 以下を追加
export GOOGLE_API_KEY="AIzaSyBs2FQS6FYWwx9LKQdyywkBFTEXt5tK9Z8"

# 設定を反映
source ~/.zshrc
```

#### 1-3. Claudeスキルに参照画像を配置（推奨）

新しいリポジトリでClaudeスキルを使用する場合：

```bash
# スキルディレクトリを作成
mkdir -p .claude/skills/kotone-business/images
mkdir -p .claude/skills/kotone-character/images
mkdir -p .claude/skills/kotone-personal/images

# 参照画像をコピー
cp docs/nanobanana-base/images/reference/* .claude/skills/kotone-business/images/
cp docs/nanobanana-base/images/reference/* .claude/skills/kotone-character/images/
cp docs/nanobanana-base/images/reference/* .claude/skills/kotone-personal/images/
```

#### 1-4. Pythonパッケージをインストール
```bash
pip3 install google-generativeai
```

詳細：[setup-guide.md](./setup-guide.md)

### Step 2: プロンプト作成

**テンプレート：**
1. [brand-foundation.md](./brand-foundation.md) の「Nanobanana用 共通プロンプト基盤」をコピー
2. 用途に応じた具体的な指示を追加
3. `prompt.txt` として保存

詳細：[usage-guide.md](./usage-guide.md)

### Step 3: 画像生成

#### 簡易スクリプトを作成
```python
import google.generativeai as genai
import os
from pathlib import Path

genai.configure(api_key=os.environ["GOOGLE_API_KEY"])
model = genai.GenerativeModel("gemini-3-pro-image-preview")

with open("prompt.txt", "r") as f:
    prompt = f.read()

response = model.generate_content(prompt)
if response.candidates and response.candidates[0].content.parts:
    Path("output.png").write_bytes(
        response.candidates[0].content.parts[0].inline_data.data
    )
    print("画像を保存しました: output.png")
```

#### 実行
```bash
python3 generate_image.py
```

詳細：[SKILL.md](./SKILL.md)

---

## 💡 使用パターン

### パターン1：ロゴを作る

#### 既存のロゴディレクトリを使う場合
1. [ロゴ生成ディレクトリ](../logo-generation/) を開く
2. `nanobanana-base/` が含まれているか確認（ない場合は取得が必要）
3. `logo_prompt.txt` を確認
4. 必要に応じてプロンプトを編集
5. `generate_logo.py` を実行
6. 1kで3パターン生成
7. 気に入ったものを4kで再生成

#### 新しいプロジェクトディレクトリを作る場合
1. プロジェクトディレクトリを作成（例：`my-logo-project/`）
2. baseを取得：
   ```bash
   # 方法1：このリポジトリからコピー
   cp -r docs/nanobanana-base my-logo-project/
   
   # 方法2：リポジトリをクローンして取得
   git clone [StudioJinseiリポジトリURL] temp
   cp -r temp/docs/nanobanana-base my-logo-project/
   rm -rf temp
   ```
3. 専用プロンプトファイルを作成
4. 生成スクリプトを作成（必要に応じて）

**注意：** baseが更新されたら、各プロジェクトディレクトリのbaseも最新版に更新してください。

### パターン2：コトネちゃんを作る
1. [kotone-character.md](./kotone-character.md) を開く
2. 基本プロンプトをコピー
3. 表情やポーズを指定
4. 参照画像を指定して生成（絵柄統一のため）

### パターン3：サイトビジュアルを作る
1. [brand-foundation.md](./brand-foundation.md) を開く
2. コトネちゃんを含める場合は [kotone-character.md](./kotone-character.md) も参照
3. 16:9または1kで生成
4. 共通プロンプト基盤 + サイト用指示

---

## 📋 チェックリスト

すべてのビジュアル制作時に確認：

- [ ] [brand-foundation.md](./brand-foundation.md) を参照したか
- [ ] カラーパレット（#A8D5BA, #1D4E4A）が正しいか
- [ ] 「シンプル、でも冷たくない」が表現されているか
- [ ] 余白がたっぷりあるか
- [ ] StudioJinseiの核心コンセプトが伝わるか
- [ ] NGデザイン（キラキラ、スピリチュアル、冷たい、チープ）になっていないか
- [ ] 判断軸（構造・迷いが減る・展望がひらく）に沿っているか

---

## 💰 料金目安

### モデル選択
| モデル | 特徴 | 料金（1k） | 用途 |
|--------|------|----------|------|
| nano_banana_pro | 高品質 | 約21-30円 | ロゴ、メインビジュアル |
| nano_banana | 高速・低コスト | 約6円 | テスト、確認用 |

### 制作例
**ロゴ制作：**
- 3パターン（1k） = 約63円
- 最終版（4k） = 約85円
- **合計：約150円**

**サイトビジュアル一式：**
- ヘッダー + コトネちゃん + セクション画像×3 + OGP画像
- **合計：約126円**

---

## 💳 API代金の確認方法と注意点

### ⚠️ 支払い設定前の確認

**Gemini APIを使うには、Google Cloud Platformで支払い設定（billing）が必要です。**

#### 1. 支払い設定の手順
1. [Google Cloud Console](https://console.cloud.google.com/billing) にアクセス
2. 「請求先アカウントを作成」をクリック
3. クレジットカード情報を登録
4. [Gemini API](https://console.cloud.google.com/apis/library/generativelanguage.googleapis.com) を有効化

#### 2. 無料枠について
- **月間無料枠**: 毎月一定量まで無料
- 詳細は [Google AI Studio 料金ページ](https://ai.google.dev/pricing) を確認

---

### 📊 API使用量の確認方法

#### 方法1：Google Cloud Consoleで確認（推奨）

```
1. https://console.cloud.google.com/billing にアクセス
2. 左メニュー「請求」→「レポート」
3. 「サービス」で「Generative Language API」を選択
4. 使用量と料金を確認
```

#### 方法2：リアルタイムモニタリング

```
1. https://console.cloud.google.com/apis/api/generativelanguage.googleapis.com/metrics にアクセス
2. リクエスト数とエラー率をモニタリング
```

---

### 🚨 支払いでびっくりしないための注意点

#### 1. 予算アラートを設定（必須）

```
手順：
1. https://console.cloud.google.com/billing にアクセス
2. 左メニュー「予算とアラート」
3. 「予算を作成」をクリック
4. 予算額を設定（例：月1,000円）
5. アラートのしきい値を設定（例：50%, 80%, 100%）
6. メール通知を有効化
```

**推奨設定例：**
- 予算額：月1,000円〜3,000円
- アラート：50%（500円）、80%（800円）、100%（1,000円）

#### 2. コスト管理のベストプラクティス

**テストは低解像度で：**
```python
# ❌ 最初から高解像度
model.generate_content("4K image...")  # 約85円

# ✅ まず低解像度でテスト
model.generate_content("1K image...")  # 約21円
# 気に入ったら高解像度で再生成
```

**プロンプトを保存：**
```python
# 同じプロンプトで何度も生成しない
# プロンプトファイルを保存してバージョン管理
```

**生成回数を記録：**
```python
# スクリプトに生成回数カウンターを追加
count = 0
for prompt in prompts:
    count += 1
    print(f"生成 {count} 枚目: 推定{count * 21}円")
    model.generate_content(prompt)
```

#### 3. 想定外の課金を防ぐチェックリスト

- [ ] Google Cloud Platformで予算アラートを設定した
- [ ] メール通知を有効にした
- [ ] 毎週金曜日に使用量を確認する習慣をつけた
- [ ] テストは必ず低解像度（1k）で行う
- [ ] 本番生成前に枚数と料金を計算する
- [ ] API使用量ダッシュボードをブックマークした

#### 4. 月間コスト予測

**StudioJinseiの想定使用量（月間）：**

| 用途 | 枚数/月 | 単価 | 月額 |
|------|---------|------|------|
| ロゴテスト | 10枚 | 21円 | 210円 |
| ロゴ最終版 | 2枚 | 85円 | 170円 |
| コトネちゃん | 5枚 | 21円 | 105円 |
| サイト画像 | 10枚 | 21円 | 210円 |
| **合計** | **27枚** | - | **約695円** |

**安全マージンを含めた推奨予算：月1,500円〜2,000円**

---

### 📱 Google AI Studio（無料・無制限）の活用

**支払い設定前、または予算を使いたくない場合：**

1. [Google AI Studio](https://aistudio.google.com/) にアクセス
2. プロンプトを貼り付けて生成
3. 生成画像をダウンロード

**メリット：**
- 完全無料（透かし入りの場合あり）
- 支払い設定不要
- クレジットカード登録不要

**デメリット：**
- 手動操作が必要
- 1日の生成枚数に制限あり
- スクリプト化できない

---

### 🔗 参考リンク

- [Google Cloud Billing Console](https://console.cloud.google.com/billing)
- [Gemini API Pricing](https://ai.google.dev/pricing)
- [Google AI Studio](https://aistudio.google.com/)
- [API使用量ダッシュボード](https://console.cloud.google.com/apis/api/generativelanguage.googleapis.com/metrics)

---

## 🔗 関連資料

### このディレクトリ内
- [ブランド共通デザイン土台](./brand-foundation.md)
- [コトネちゃん設定](./kotone-character.md)
- [セットアップガイド](./setup-guide.md)
- [使い方ガイド](./usage-guide.md)

### 実制作ディレクトリ（このベースを参照）
- [ロゴ生成](../logo-generation/) - ロゴ制作用ディレクトリ（このベースを参照）

### 参考リポジトリ・資料
- [reference-nanobanana](../reference-nanobanana/) - 師匠（dataanalytics2020）提供のオリジナル版（参考資料）

### 外部資料
- [会社コンセプト](../opening-preparation/strategy/company-concept.md)
- [デザインコンセプト](../opening-preparation/strategy/design-concept.md)
- [brand-visualizer skill](../.claude/skills/brand-visualizer/SKILL.md)

---

## 📝 変更があった場合

**このStudioJinseiリポジトリのnanobanana-baseディレクトリだけを更新すればOK！**

```bash
cd ~/Desktop/StudioJinsei
git pull
```

すべての設定・プロンプト・ガイドがこのディレクトリに含まれているので、他のリポジトリは不要です。

### ⚠️ プロジェクトディレクトリでのbaseの取得方法

各プロジェクトディレクトリ（`logo-generation/`等）でbaseを使用する場合：

#### 方法1：元のリポジトリからクローン（推奨）

```bash
# プロジェクトディレクトリ内で
cd your-project-directory
git clone [StudioJinseiリポジトリURL] temp
cp -r temp/docs/nanobanana-base .
rm -rf temp
```

#### 方法2：最新版を手動で入れる

元のリポジトリ（`docs/nanobanana-base/`）から最新版をコピー：

```bash
# 元のリポジトリから
cd ~/Desktop/StudioJinsei/docs
cp -r nanobanana-base /path/to/your-project-directory/
```

#### 方法3：リポジトリ内にない場合

プロジェクトディレクトリ内に `nanobanana-base/` がない場合は、上記の方法1または方法2で取得してください。

**注意：** baseが更新されたら、各プロジェクトディレクトリのbaseも最新版に更新することを推奨します。

---

## 🎓 Tips

### プロンプト作成のコツ
1. **必ず共通プロンプト基盤を含める**
   - [StudioJinsei Brand Foundation] セクション
2. **カラーコードを明記**
   - #A8D5BA (ソフトミント), #1D4E4A (ダークティール)
3. **避けるべきものを明記**
   - Avoid: flashy, overly colorful, spiritual vibes, etc.
4. **参照画像を活用**
   - 絵柄統一のため、既存画像を参照画像に指定

### コスト最適化
1. **テストは1k**で行う
2. **確定した最終版のみ4k**で生成
3. **まとめて生成**してコマンド実行回数を減らす

### 品質管理
1. **生成後は必ずチェックリスト確認**
2. **プロンプトファイルを保存**してバージョン管理
3. **参照画像のパスを記録**

---

**最終更新：2025/12/20**
