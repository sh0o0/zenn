---
title: "GitHub Copilotを完全自走させるための3つの設定"
emoji: "🏃‍➡️"
type: "idea"
topics: ['vscode', 'githubcopilot']
published: false
---

こんにちは 👋
GitHub Copilot を愛用している[@sho](https://x.com/sh0o0000)です。

GitHub Copilotをもっと便利に使いたいと思ったことはありませんか？この記事では、Copilotの設定を最適化して生産性を向上させる3つのステップをご紹介します。

## 背景

最近、Claude Sonnet 4が登場し、タスクを粘り強く完遂しようとする能力が向上しました。しかし、コマンドやツールの承認（approve）やイテレーションが長引くと、「まだタスクを続けますか？」と確認されることが増え、結果的にチャットに張り付く必要が出てきてしまいました。

このような状況を改善するために、GitHub Copilotの設定を最適化し、よりスムーズな作業環境を構築する方法を模索しました。この記事では、その具体的な手順をご紹介します。

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

`.devcontainer/devcontainer.json`:

```json
{
  "name": "Node.js & TypeScript",
  "build": {
    "dockerfile": "${localWorkspaceFolder}/.devcontainer/Dockerfile", // Dockerfile内でgo downloadなどを実行
    "options": [
      "--network",
      "host" // build時のみネットワークを有効にする
    ]
  },
  "runArgs": [
    "--network",
    "no-internet" // コンテナ起動時はネットワークを無効にする
  ],
  "customizations": {
    "vscode": {
      "chat.tools.autoApprove": true,
      "workbench.colorTheme": "Solarized Dark"
    }
  }
}
```

<!-- TODO: 検証が必要 -->
`.devcontainer/Dockerfile`:

```dockerfile
FROM mcr.microsoft.com/devcontainers/typescript-node:1-22-bookworm

# 必要なパッケージをインストール
RUN npm install
```

## まとめ

これらの設定を活用することで、GitHub Copilotのパフォーマンスを最大限に引き出すことができます。ぜひ試してみてください！

タスク完了時に音を鳴らすようにしておくとさらに便利です。音の設定方法は以下の記事を参考にしてください：
https://zenn.dev/nakar0/articles/20250603_vscode-copilot-sound
