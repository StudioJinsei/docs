# リポジトリ名変更ガイド

**作成日：2025/12/20**

`docs` リポジトリの名前を変更する手順です。

---

## 🎯 変更理由

- `docs` という名前は他のリポジトリの `docs/` ディレクトリと混同しやすい
- より明確なリポジトリ名にすることで、識別しやすくなる

---

## 📝 推奨リポジトリ名

以下のいずれかを推奨：

1. **`studiojinsei-docs`** - シンプルで明確
2. **`studiojinsei-manuals`** - manualsが主な内容なので
3. **`studiojinsei-knowledge`** - 知識ベースとしての位置づけ

---

## 🔄 リポジトリ名変更手順

### Step 1: GitHubでリポジトリ名を変更

1. GitHubのリポジトリページにアクセス
2. 「Settings」タブを開く
3. ページ最下部の「Danger Zone」セクションを開く
4. 「Change repository name」をクリック
5. 新しいリポジトリ名を入力（例：`studiojinsei-docs`）
6. 確認して変更

### Step 2: ローカルのリモートURLを更新

```bash
# 現在のリモートURLを確認
cd ~/Desktop/StudioJinsei/docs
git remote -v

# リモートURLを更新
git remote set-url origin https://github.com/[ユーザー名]/studiojinsei-docs.git

# 確認
git remote -v
```

### Step 3: 他のリポジトリやドキュメントの参照を更新

以下のファイルでリポジトリURLを更新：

- `nanobanana-base/README.md` - GitHubリポジトリ情報セクション
- `nanobanana-base/setup-guide.md` - クローンコマンド
- `nanobanana-base/SKILL.md` - 自動セットアップ手順
- その他、リポジトリURLを参照しているファイル

**検索コマンド：**
```bash
# リポジトリURLを参照している箇所を検索
grep -r "github.com.*StudioJinsei" .
```

### Step 4: 他のリポジトリからの参照を更新

他のリポジトリ（`line`、`brand`等）からこのリポジトリを参照している場合、それらも更新：

```bash
# 他のリポジトリで
cd ~/Desktop/StudioJinsei/line
git remote set-url origin https://github.com/[ユーザー名]/studiojinsei-docs.git
```

---

## ⚠️ 注意点

1. **既存のクローン済みリポジトリ**
   - 他のマシンや環境でクローン済みの場合は、リモートURLを更新する必要があります

2. **CI/CDや自動化スクリプト**
   - リポジトリURLを参照しているスクリプトがあれば更新が必要

3. **ドキュメント内の参照**
   - すべてのドキュメントでリポジトリURLを検索して更新

---

## ✅ 変更後の確認

```bash
# リモートURLが正しく更新されているか確認
git remote -v

# プッシュできるか確認
git push origin main
```

---

**最終更新：2025/12/20**

