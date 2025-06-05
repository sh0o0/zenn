---
title: "GitHub Copilotを最大限に活用する方法"
emoji: "🚀"
type: "idea"
topics: ['vscode', 'githubcopilot']
published: false
---

こんにちは 👋
GitHub Copilot Chatを愛用している[@sho](https://x.com/sh0o0000)です。

GitHub Copilotをもっと便利に使いたいと思ったことはありませんか？この記事では、Copilotの設定を最適化して生産性を向上させる3つのステップをご紹介します。

## 概要

1. Auto Approve を有効にする
2. Max Requests を増やす
3. Dev Containersで安全な環境を構築する

## 手順

### 1. Auto Approve を有効にする

Copilotの提案を自動承認することで、作業のスピードを大幅に向上させることができます。

1. `CMD + ,` またはコマンドパレットから設定を開きます。
2. 検索バーに「auto approve」と入力します。
3. `Auto Approve`にチェックを入れます。

![Auto Approve 設定](/images/20250605_vscode-copilot-auto/auto-approve.png)

### 2. Max Requests を増やす

Copilotが一度に処理できるリクエスト数を増やすことで、よりスムーズな体験が可能になります。

1. `CMD + ,` またはコマンドパレットから設定を開きます。
2. 検索バーに「max requests」と入力します。
3. `Max Requests`の値を増やします（デフォルトは25、私は100に設定しています）。

![Max Requests 設定](/images/20250605_vscode-copilot-auto/max-requests.png)

### 3. Dev Containersで安全な環境を構築する

設定を適用するだけでなく、Dev Containersを使って作業環境を隔離することで、より安全に利用できます。

以下はNode.js & TypeScriptのDev Container設定例です：

`.devcontainer/devcontainer.json`:

```json
{
  "name": "Node.js & TypeScript",
  "image": "mcr.microsoft.com/devcontainers/typescript-node:1-22-bookworm",
  "customizations": {
    "vscode": {
      "extensions": [
        "installしたいextensionのID" // 例: "biomejs.biome"
      ],
      "settings": {
        "chat.tools.autoApprove": true,
        "workbench.colorTheme": "Solarized Dark"
      }
    }
  }
}
```

さらに、ネットワークからも隔離するには以下のコマンドと設定を使用します：

```fish
docker network create --internal --driver bridge no-internet
```

Go言語のDev Container設定例も参考にしてください：

`.devcontainer/devcontainer.json`:

```json
{
  "name": "Go",
  "image": "mcr.microsoft.com/devcontainers/go:1-1.23-bookworm",
  "features": {
    "ghcr.io/jungaretti/features/make:1": {},
    "ghcr.io/guiyomh/features/golangci-lint": {
      "version": "1.64.8"
    }
  },
  "postCreateCommand": "go version",
  "customizations": {
    "vscode": {
      "chat.tools.autoApprove": true
    }
  }
}
```

## まとめ

これらの設定を活用することで、GitHub Copilotのパフォーマンスを最大限に引き出すことができます。ぜひ試してみてください！

タスク完了時に音を鳴らすようにしておくとさらに便利です。音の設定方法は以下の記事を参考にしてください：
https://zenn.dev/nakar0/articles/20250603_vscode-copilot-sound
