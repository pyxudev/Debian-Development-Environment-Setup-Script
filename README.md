# Debian Development Environment Bootstrap Script

新規にインストールした **Debian 環境** に対して、  
**開発に必要なツール・設定を一括でセットアップ**するためのスクリプトです。

- 初回マシンセットアップを高速化
- 手動設定ミスを防止
- 冪等性を意識した安全な実装
- ログ出力対応（トラブルシュートしやすい）

---

## ✨ Features

- APT / Snap による基本ツールのインストール
- Docker / Docker Compose のセットアップ
- docker グループの存在・所属チェック（安全）
- Git global config（user.name / user.email）の対話設定
- sudo 実行権限の事前チェック
- エラー時にターミナルが即終了しない UX
- 全実行ログを `install.log` に保存

---

## 📦 Installed Tools (example)

- git
- curl / wget
- Docker / Docker Compose
- Node.js / pnpm
- Terraform
- Databases (PostgreSQL / Redis)
- その他 開発に必要な基本パッケージ

※ 実際の内容は `install.sh` を参照してください。

---

## 🚀 Usage

### 1. リポジトリを取得

```bash
git clone <this-repository>
cd <this-repository>
```

### 2. 実行権限を付与

```bash
chmod +x install.sh
```

### 3. スクリプト実行（一般ユーザーで）

```bash
./install.sh
```

⚠️ **root では実行しないでください**

---

## 🔐 sudo 権限について

このスクリプトは `sudo` を使用します。

### sudo が使えない場合

以下のメッセージを表示して安全に終了します：

```text
[ERROR] sudo is NOT available for user
Please run the following commands as root:
  su -
  usermod -aG sudo <username>
```

管理者で以下を実行してください：

```bash
su -
usermod -aG sudo <username>
reboot
```

再ログイン後にスクリプトを再実行してください。

---

## 📝 Git Global Config

初回実行時、以下を **対話形式** で設定します：

- `git config --global user.name`
- `git config --global user.email`

すでに設定されている場合はスキップされます。

---

## 📄 Logs

すべての標準出力・標準エラーはログに保存されます。

```text
~/install.log
```

ログ例：

```text
======== install started: 2026-01-26 14:32:10 ========
[INFO] docker group already exists
[INFO] user 'user' is already in docker group
```

---

## 🧠 Design Policy

- 冪等性を重視（再実行しても壊れにくい）
- `set -e` 環境でも安全に動作
- 対話 / 非対話の両対応
- 失敗時も「次に何をすべきか」を明示

---

## ⚠️ Notes

- Docker グループ追加後は **ログアウト / 再ログイン** が必要です。
- 環境にて実行した際に問題が発生した場合は Issue をあげてください。

---

## 📌 Recommended Extensions

- SSH key 自動生成
- GitHub CLI (`gh`) セットアップ
- dotfiles 管理（chezmoi / yadm）
- cloud-init 対応
