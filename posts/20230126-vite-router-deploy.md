---
title: 如何將 Vite + Vue-Roueter 專案部署到 Github Pages
description: 使用 Vite + Vue-Router 如何部署到 Github Pages
slug: 20230126-vite-router-deploy
date: 2023-01-26
type: Post
socialImage:
---

## 前言

記錄關於 Vite + Vue-Router 專案部署到 Github Pages 上的流程。

## 環境建立

首先將整個專案推送到 main / master 分之

```bash
# 初始化 git 並建立新的本地端 repository。
git init

# 使用 .(--all) 將所有檔案加入追蹤
git add .

# 提交目前的儲存的異動，並透過 `-m` 參數設定摘要說明文字。
git commit -m "initial"

# 這行可以選擇不要執行
# 主要是將你的 master 分之改名為 main
# 一但改名了，後面都要跟著改動
git branch -M main

# 添加遠端數據庫
git remote add origin <遠端儲存庫 url>

# 推送到你的遠端數據庫
# 並使用 -u 參數將預設的遠端儲存庫為 origin
# origin 為預設遠端儲存庫的參照名稱
git push -u origin main
```

建立好環境後安裝需要手動安裝 Vue-Router。

```bash
npm install vue-router@

# yarn 
yarn add vue-router@
```

環境都建立好後，接下來











 