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

# 使用 .(-all) 
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/CofCat456/vite-router-demo.git
git push -u origin main
```

建立好環境後安裝需要手動安裝 Vue-Router。

```bash
npm install vue-router@

# yarn 
yarn add vue-router@
```

環境都建立好後，接下來











 