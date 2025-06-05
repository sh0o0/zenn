---
title: "WIP"
emoji: "🤖"
type: "idea"
topics: ['vscode', 'githubcopilot']
published: false
---

こんにちは 👋
GitHub Copilot Chatを愛用している[@sho](https://x.com/sh0o0000)です。

## 概要

1. Auto Approve を有効にする
2. Max Requests を増やす
3. Dev Containersで環境を閉じる

## 手順

### 1. Auto Approve を有効にする

1. `CMD + ,` or コマンドパレットから設定を開く
2. 検索バーに「auto approve」と入力する
3. `Auto Approve`にチェックを入れる
![settings](/images/20250605_vscode-copilot-auto/auto-approve.png)

### 2. Max Requests を増やす

1. `CMD + ,` or コマンドパレットから設定を開く
2. 検索バーに「max requests」と入力する
3. `Max Requests`の値を増やす（デフォルトは25、私は100にしています）
![settings](/images/20250605_vscode-copilot-auto/max-requests.png)

### 3. Dev Containersで環境を閉じる

自走はこれまでの設定で完了ですが、変な挙動をするのが怖いのでDev Containersを使って環境を閉じることをお勧めします。

私はAuto ApproveはDev Containersでのみ有効にしています。
またcolorThemeを設定しておくとVSCodeの色でDev Containersで識別できるので便利です。

Node.js & TypeScriptのDev Container設定は以下のようになります。

`.devcontainer/devcontainer.json`:

```json
{
  "name": "Node.js & TypeScript",
  "image": "mcr.microsoft.com/devcontainers/typescript-node:1-22-bookworm",
  "customizations": {
    "vscode": {
      "extensions": [
        // GitHub Copilotは自動でインストールされます
        "installしたいextensionのID", // 例: "biomejs.biome",
        ...
      ],
      "settings": {
        "chat.tools.autoApprove": true,
        "workbench.colorTheme": "Solarized Dark"
      }
    }
  }
}
```

## ネットワークからも隔離

docker network create --internal --driver bridge no-internet
```json
// For format details, see https://aka.ms/devcontainer.json. For config options, see the
// README at: https://github.com/devcontainers/templates/tree/main/src/go
{
  "name": "Go",
  "image": "mcr.microsoft.com/devcontainers/go:1-1.23-bookworm",
  // "build": {
  //   "dockerfile": "${localWorkspaceFolder}/.devcontainer/Dockerfile",
  //   "args": {
  //     "WORKSPACE_FOLDER": "${containerWorkspaceFolder}"
  //   },
  //   "options": [
  //     "--network",
  //     "host"
  //   ]
  // },
  "features": {
    "ghcr.io/jungaretti/features/make:1": {},
    "ghcr.io/guiyomh/features/golangci-lint": {
      "version": "1.64.8"
    }
  },
  // "runArgs": [
  //   "--network",
  //   "no-internet"
  // ],
  "postCreateCommand": "go version",
  "customizations": {
    "vscode": {
      "chat.tools.autoApprove": true
    }
  }
}

```

完了時に音を鳴らすようにしておくと便利
https://zenn.dev/nakar0/articles/20250603_vscode-copilot-sound
