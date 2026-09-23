# setup-mac

新しい Mac に全社標準アプリを一括インストールするための Brewfile。

**これは土台であり、完成形ではない。** 業務に必要なツールは各自で追加して使う。

## 導入

### 1. Homebrew をインストール

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Apple Silicon の場合、インストール後に PATH を通す。

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile && eval "$(/opt/homebrew/bin/brew shellenv)"
```

### 2. リポジトリを取得

```bash
git clone https://github.com/Achroma-inc/setup-mac.git && cd setup-mac
```

### 3. アプリを一括インストール

```bash
brew bundle install --file=Brewfile
```

管理者パスワードを数回求められる。

### 4. インストール確認

```bash
brew bundle check --file=Brewfile
```

`Brewfile dependencies are satisfied.` と出れば完了。

## 収録アプリ

| アプリ | cask | 用途 |
| ---- | ---- | ---- |
| Google Chrome | `google-chrome` | ブラウザ |
| Slack | `slack` | 社内チャット |
| Zoom | `zoom` | 会議 |
| Microsoft Teams | `microsoft-teams` | 会議・チャット |
| Microsoft Excel | `microsoft-excel` | 表計算 |
| Microsoft PowerPoint | `microsoft-powerpoint` | 資料作成 |
| Microsoft Word | `microsoft-word` | 文書作成 |
| Notion | `notion` | ドキュメント |
| Visual Studio Code | `visual-studio-code` | エディタ |
| Claude | `claude` | AI |
| Rectangle | `rectangle` | ウィンドウ管理 |

## 手動インストールが必要なもの

### Bluedot

Homebrew に cask が存在しないため、公式サイトから取得する。

https://bluedothq.com/

## 初回サインイン

| アプリ | 方法 |
| ---- | ---- |
| Chrome | Google アカウント (SSO) |
| Slack | SSO |
| Zoom | SSO |
| Teams / Excel / PowerPoint / Word | Microsoft 365 アカウント (SSO) |
| Notion | SSO |
| Claude | 会社アカウント |
| Bluedot | 会社アカウント |

Rectangle と VS Code はサインイン不要。VS Code の設定は Settings Sync で引き継げる。

## 補足

- 全 cask が `auto_updates` に対応しており、アプリ自身が自動更新する。`brew upgrade` での一括更新は基本不要
- Office は Excel / PowerPoint / Word を個別 cask で入れている。`microsoft-office` でまとめると Outlook・OneNote・OneDrive も付いてくるため、標準構成はこの3本とする

## 収録アプリへの変更

全社に影響するため PR を出してレビューを受ける。

1. `Brewfile` と本 README を編集する
2. `brew info --cask <name>` で cask 名が解決できることを確認する
3. PR を出す

### 何を Brewfile に入れるか

- **入れる**: 全社員が業務で使うアプリ
- **入れない**: 個人の好みのツール、特定業務でしか使わないもの、ローカル環境固有の設定

個人で使うものは各自の Brewfile に置く。複数人が同じものを個別に入れていると分かった時点で全社へ引き上げる。
