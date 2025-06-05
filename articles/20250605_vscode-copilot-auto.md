---
title: "GitHub Copilotを完全自走させるための3つの設定"
emoji: "🏃"
type: "idea"
topics: ['vscode', 'githubcopilot']
published: false
---

こんにちは 👋
GitHub Copilot を愛用している[@sho](https://x.com/sh0o0000)です。

GitHub Copilotを完全自走させたいと思ったことはありませんか？この記事では、Copilotの設定を最適化し、手放しで作業を進められる3つのステップをご紹介します。

## 背景

最近、Claude Sonnet 4が登場し、タスクを粘り強く完遂しようとする能力が向上しました。しかし、コマンドやツールの承認やイテレーションが長引くと、「まだタスクを続けますか？」と確認されることが増え、結果的にチャットに張り付く必要が出てきてしまいました。

このような状況を改善するために、GitHub Copilotの設定を最適化し、完全自走を目指す方法を模索しました。この記事では、その具体的な手順をご紹介します。

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

設定を適用するだけでなく、[Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)を使って作業環境を隔離することで、より安全に利用できます。
私はAuto ApproveはDev Container内でのみ有効にするようにしています。

以下はNode.js & TypeScriptのDev Container設定例です：

`.devcontainer/devcontainer.json`:

```json
{
  "name": "Node.js & TypeScript",
  "image": "mcr.microsoft.com/devcontainers/typescript-node:1-22-bookworm",
  "customizations": {
    "vscode": {
      "settings": {
        "chat.tools.autoApprove": true, // Auto Approveを有効にする
        "workbench.colorTheme": "Solarized Dark" // Dev Container用のテーマを設定しておくと見やすい
      },
      "extensions": [
        "installしたいextensionのID" // 例: "biomejs.biome"
      ]
    }
  }
}
```

## まとめ

これらの設定を活用することで、GitHub Copilotを完全自走させることができます。ぜひ試してみてください！

タスク完了時に音を鳴らすようにしておくとさらに便利です。音の設定方法は以下の記事を参考にしてください：
https://zenn.dev/nakar0/articles/20250603_vscode-copilot-sound
