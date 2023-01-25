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

## 部屬到 Github

### 設定

在推送前需要

### 推送專案

首先將整個專案推送到 main / master 分支

```bash showLineNumbers {13, 16, 21}
# 初始化 git 並建立新的本地端 repository。
git init

# 使用 .(--all, -A) 將所有檔案加入追蹤
git add .

# 提交目前的儲存的異動，並透過 `-m` 參數設定摘要說明文字。
git commit -m "initial"

# 這行可以選擇不要執行
# 主要是將你的 master 分支改名為 main
# 一但改名了，後面都要跟著改動
git branch -M main

# 添加遠端數據庫
git remote add origin <遠端儲存庫 url>

# 推送到你的遠端數據庫
# 並使用 -u 參數將預設的遠端儲存庫為 origin
# origin 為預設遠端儲存庫的參照名稱
git push -u origin main
```

這樣就將整個專案推送到 Github 的 Repository 上了。

順帶一提，`commit` 時如果不帶 `-m` 參數的話，會進入到 vi 或 vim 編輯器中，一樣能進行 `commit` ，不過可能會遇到出不來、不能打字的問題，這又是另一段故事了...

但目前我們的專案還沒辦法掛到 GitHub Pages 上。
我們真正要掛載的是，打包出來的檔案。

而我們目標是掛載到 `gh-pages` 這個分支上，這樣 GitHub Pages 會自動找到這個分支，並掛載他。

這裡我們使用官方所推薦的方式來部署，在[官方的文件](https://vitejs.dev/guide/static-deploy.html#github-pages) 提到需要創建一個 `deploy.sh` 脚本。

>腳本簡單說就是將上面使用過的密密麻麻指令放在腳本裡，當執行腳本時，就會自動執行腳本內的指令。

腳本內容如下
要特別注意的是，如果主分支是 `master` 的話，記得要換掉腳本中所有的 `main`。

```bash
#!/usr/bin/env sh

# abort on errors
set -e

# build
# 將專案打包
npm run build

# navigate into the build output directory
cd dist

# place .nojekyll to bypass Jekyll processing
echo > .nojekyll

# if you are deploying to a custom domain
# echo 'www.example.com' > CNAME

git init

# 根據本人觀察，這行大多人都會選擇註解掉，影響不大
# git checkout -B main

git add -A
git commit -m 'deploy'

# 如果你要部署在 https://<USERNAME>.github.io
# git push -f git@github.com:<USERNAME>/<USERNAME>.github.io.git main

# 一般使用都是選擇這個
# 如果你要部署在 https://<USERNAME>.github.io/<REPO>
git push -f git@github.com:<USERNAME>/<REPO>.git main:gh-pages

cd -
```

接下來就可以到 Github 上查看是否有兩個分支，並且是否都有成功上傳。

## 參考

- [30 天精通 Git 版本控管 (25)：使用 GitHub 遠端儲存庫 - 觀念篇](https://ithelp.ithome.com.tw/articles/10140055) iThome 鐵人賽
- [Git & GitHub 教學手冊](https://w3c.hexschool.com/category/repo) W3Hexschool












 