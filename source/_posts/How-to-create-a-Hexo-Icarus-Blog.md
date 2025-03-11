---
title: Hexo Icarus 架站紀錄
date: 2025-03-01 20:16:35
tags:
  - Hexo
  - Blog
  - Icarus
---

## 前言

開始習慣了 Markdown 寫文件後，越來越覺得 Medium 不適合用來整理技術筆記，還是另尋空間，並終於在 2025 初用 Hexo 架了自己的 blog。

Hexo 有很多開源主題，原先我是無腦跟著 [胡立使用 Minos 這個主題](https://www.facebook.com/huli.blog/posts/pfbid0iW4WWd4yw2fZYT1N7ptEkzJb2WaLqpjKARZ1eRjhfwp2Z3udfBc9SKtK46zGb5ool)，但後來發現安裝過程出現問題，且 [Minos 的 GitHub](https://github.com/ppoffice/hexo-theme-minos) 也在 2022 年進入 read-only 狀態，不開放提 issue，決定轉向其他還在維護中的 theme。

目前最熱門的 Hexo 主題除了 [NexT](https://github.com/theme-next/hexo-theme-next) 以外，也看到有人在推薦使用 [Icarus](https://github.com/ppoffice/hexo-theme-icarus)。後者的星星數沒有 NexT 那麼高，以順眼程度來說我還是選擇了 Icarus。

---

## 流程

接下來紀錄我的架站過程。請記得用 `node -v`, `npm -v` 跟 `git` 檢查工具是否已經安裝好，再進行後續步驟。

---

### 1. 安裝 Hexo

#### 1-1. 全局安裝 hexo-cli

```bash
npm install -g hexo-cli
```

💡 **提示:**  
Mac 使用者可以用 `npm list -g --depth=0` 看到已經被全局安裝。

---

#### 1-2. 安裝 Hexo

將 `<folder>` 換成自己想要的名稱：

```bash
hexo init <folder>
cd <folder>
npm install
```

---

#### 1-3. 檢查是否安裝完成

用 `hexo server` 或 `hexo s` 並到 [http://localhost:4000](http://localhost:4000) 檢查，當看到預設的網站配置，代表安裝完成。

![圖片](./img/How-to-create-a-Hexo-Icarus-Blog-1.png)

---

### 2. 推送至遠端 Git Repo

到這為止，可以在 GitHub 建立個人 repo 並且推送。  
必須設為公開才能加入 Discussion 留言版功能。

---

### 3. 安裝 Icarus 主題

Icarus 官方 Blog ["Getting Started with Icarus"](https://ppoffice.github.io/hexo-theme-icarus/uncategorized/getting-started-with-icarus/) ([中文版](https://ppoffice.github.io/hexo-theme-icarus/uncategorized/icarus%E5%BF%AB%E9%80%9F%E4%B8%8A%E6%89%8B/)) 提供兩種安裝方式: Install from source 或 Install via NPM。

我比較推薦用 **Install from source (`git clone`)**，因為大部分的 Blog 教學都是以這個為基礎來做配置。若使用 `npm install`，Icarus 會被當作 NPM package 來安裝，資料夾結構會長得跟 `git clone` 不太一樣，發生問題也比較少資源可以查詢。

---

#### 3-1. 使用 Install from source

官方部落格有介紹兩種方法，選一種使用就好了。

**方法一：獨立的 repo （我是選這個）**

```bash
git clone https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus --depth 1
```

💡 **提示:**  
- 若指定版本，可使用 `-b <version number>`，不指定就是 latest 版本。  
- `--depth 1` 代表只下載最新的 commit，不包含完整的 commit 歷史。  
- 使用這個方法後，須透過 `git rm --cached themes/icarus` 移除嵌套的 git repo，之後使用 `git add .` 才不會出現錯誤訊息。

---

**方法二：加入為 submodule**

```bash
git submodule add https://github.com/ppoffice/hexo-theme-icarus.git themes/icarus
```

💡 **提示:**  
加入後，使用 `git submodule status` 可以看到子模組的資訊。

---

#### 3-2. 設定 theme

```bash
hexo config theme icarus
```

💡 **提示:**  
這跟手動更改根資料夾中的 `_config.yml` 中的 `theme: icarus` 是一樣的意思。

---

#### 3-3. 使用 `hexo generate && hexo server` 檢查安裝成功

![image](https://hackmd.io/_uploads/B1y8-rJYyx.png)

---

💡 **安裝過程中有遇到問題:**  
見這篇 [GitHub Discussion](https://github.com/ppoffice/hexo-theme-icarus/issues/1340)

