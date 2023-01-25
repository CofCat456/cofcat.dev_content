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

## 部屬流程

在推送前，需要先進行環境的設定，這樣檔案推送上去後，才能順利找到掛載上去的檔案。

### 設定

- vite.config
  首先需要先確認專案底下是否有 `vite.config.js` 的檔案，沒有的話請建立一個，接著我們需要將 Repository 的名稱加入設定檔中。
  
```javascript showLineNumbers {6}
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  base: '/REPO/',
  plugins: [vue()],
})

```

這樣就設定完 Vite

- Vue-Router
  接下來需要設定 `router` 的 `base path`，不設定的話，可能會造成掛載後，router 路徑錯誤或是找不到頁面的問題。

```javascript showLineNumbers {5}
import { createRouter, createWebHistory } from 'vue-router';
import HelloWrold from '../components/HelloWorld.vue';
import RouterTest from '../components/RouterTest.vue';

const history = createWebHistory('/REPO/');
const routes = [
  {
    path: '/',
    name: 'Hello',
    component: HelloWrold
  },
  {
    path: '/test',
    name: 'RouterTest',
    component: RouterTest
  }
];

export default createRouter({ history, routes });

```

都設定好後就可以進入部署的環節。

### 部署

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

```bash showLineNumbers {32}
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

![[截圖 2023-01-26 上午4.12.44.png]]

等待大概 5 分鐘就可以查看是否有部署成功囉！

### 環境

當推送完後，很開心想要馬上進行修改的同時，會注意到專案在本地端運行時，會有點不一樣。

![[截圖 2023-01-26 上午4.17.28.png]]

這是因為我們剛剛已經對 `router` 的 `base path` 進行修改。

現在我們要加入一些判斷，來讓設定檔只有正式環境中才需要進行修改。

- vite.config
```javascript showLineNumbers
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  base: process.env.NODE_ENV === 'production' ? '/vite-router-demo/' : '',
  plugins: [vue()],
})

```

這裡我們透過 `process.env.NODE_ENV` 的方式來得知當前的

這是因為

## 參考

- [30 天精通 Git 版本控管 (25)：使用 GitHub 遠端儲存庫 - 觀念篇](https://ithelp.ithome.com.tw/articles/10140055) iThome 鐵人賽
- [Git & GitHub 教學手冊](https://w3c.hexschool.com/category/repo) W3Hexschool












 