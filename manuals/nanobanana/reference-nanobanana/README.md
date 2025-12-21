# Nanobanana Skill（師匠オリジナル版）

**保存日：2025/12/20**

📂 [manuals READMEに戻る](../../README.md)

---

## 📖 概要

師匠（dataanalytics2020）からプルリク #1 でもらった、Nanobanana Pro を使用した画像生成スキルのオリジナル版です。

**プルリク情報：**
- PR #1: `feat: Claude Code用nanobanana-comic-creatorスキルを追加`
- 日付: 2025-12-18
- Author: dataanalytics2020

---

## 📁 ファイル一覧

### 1. SKILL-original.md
メインのスキル定義ファイル。Nanobanana Proを使った画像生成の使い方が記載されています。

**含まれる内容：**
- 4コマ漫画生成
- キャラクター画像生成
- ロゴ生成
- セットアップ方法

### 2. slomap-characters.md
**さがすちゃん**等のキャラクター設定ファイル。

**登場キャラクター：**
- 🐱 ネコ「サガすちゃん」- ユーザー代表、一緒に探す相棒
- 🐻 クマ「ガイドくん」- AI/ガイド担当、頼れる案内役
- 🐰 ウサギ「ミミちゃん」- 情報収集担当、耳が大きくて情報キャッチが得意

**アートスタイル：**
- ソシャゲ風（ゲーム風）
- シャープな線、鮮やかなグラデーション
- キラキラエフェクト

### 3. nanobanana-usage.md
Nanobanana Proの詳細な使い方ガイド。

---

## 🔧 セットアップ（参考）

### 必要なもの
1. [slomap-note-automation](https://github.com/dataanalytics2020/slomap-note-automation) リポジトリ
2. Google API Key

### 環境変数設定
```bash
export GOOGLE_API_KEY="your-api-key"
export NANOBANANA_REPO_PATH="$HOME/Desktop/slomap-note-automation"
```

### 基本的な使い方
```bash
# 基本コマンド（1k解像度推奨）
python scripts/nanobanana.py prompts/my_prompt.md -r 1k

# 参照画像付き（絵柄統一）
python scripts/nanobanana.py prompts/my_prompt.md -r 1k -i "images/reference.png"
```

---

## 💡 StudioJinseiでの活用

このスキルを参考に、StudioJinsei用のブランドビジュアル生成スキル（brand-visualizer）を作成しました。

- 参照: `/Users/rin5uron/Desktop/StudioJinsei/docs/.claude/skills/brand-visualizer/SKILL.md`

---

## 🔗 関連資料

- [manuals README](../README.md)
- [nanobanana-base](../nanobanana-base/) - StudioJinsei用のベースディレクトリ（同じnanobananaディレクトリ内）
- [brand-visualizer skill](../../.claude/skills/brand-visualizer/SKILL.md)
- [会社コンセプト](../../opening-preparation/strategy/company-concept.md)
- [デザインコンセプト](../../opening-preparation/strategy/design-concept.md)
