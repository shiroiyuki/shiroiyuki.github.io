# ゆうき's Blog (shiroiyuki.github.io) ❄️

> 這裡是 **[ゆうき (shiroiyuki)](https://shiroiyuki.github.io/)** 的個人技術筆記與二次元隨筆部落格。

![Node.js >= 22](https://img.shields.io/badge/node.js-%3E%3D22-brightgreen)
![pnpm >= 11](https://img.shields.io/badge/pnpm-%3E%3D11-blue)
![Astro](https://img.shields.io/badge/Astro-7-orange)
![TypeScript](https://img.shields.io/badge/TypeScript-6-blue)

- 🌐 **正式站點**：[https://shiroiyuki.github.io/](https://shiroiyuki.github.io/)
- 🚀 **技術架構**：[Astro 7](https://astro.build/) + [Svelte 5](https://svelte.dev/) + [Tailwind CSS 4](https://tailwindcss.com/)（基於 [Firefly](https://github.com/CuteLeaf/Firefly) 主題客製）
- 🎨 **視覺風格**：全螢幕二次元立繪壁紙、半透明毛玻璃卡片、白雪冰藍專屬圖標

---

## 🧞 常用指令速查表 (Commands)

本專案強制使用 `pnpm` 套件管理器（由 `preinstall` 腳本檢查），所有指令皆在專案根目錄下執行：

| 指令 (Command) | 功能說明 (Action) |
| :--- | :--- |
| `pnpm install` | 安裝專案依賴套件 |
| `pnpm dev` / `pnpm start` | 在 `http://localhost:4321` 啟動本地開發伺服器（支援即時熱重載） |
| `pnpm build` | 建置生產環境靜態網站至 `./dist/`（自動生成 GitHub 卡片快取、LQIP 預覽圖、VNDB 封面、字型子集與 Pagefind 搜尋索引） |
| `pnpm preview` | 在本地啟動伺服器預覽 `./dist/` 已建置完成的生產版網站 |
| `pnpm new-post <filename>` | **建立新文章**：於 `src/content/posts/` 自動生成含 Frontmatter 的 Markdown 檔案 |
| `pnpm new-d <content>` | **建立新動態（短指令）**：於 `src/content/dynamic/` 快速建立帶時間戳記的隨手動態 |
| `pnpm new-dynamic <content>` | **建立新動態（完整指令）**：與 `pnpm new-d` 功能完全相同 |
| `pnpm check` | 執行 `astro check` 進行 Astro 元件與內容型別診斷 |
| `pnpm type-check` | 執行 `tsc --noEmit --isolatedDeclarations` 進行 TypeScript 型別檢查 |
| `pnpm format` | 使用 Biome 自動格式化 `./src` 與 `./scripts` 程式碼 |
| `pnpm lint` | 使用 Biome 檢查並自動修復 `./src` 與 `./scripts` 程式碼規範問題 |
| `pnpm lqips` | 手動重新生成圖片低畫質預覽佔位圖 (`src/constants/lqips.json`) |
| `pnpm github-cards` | 手動預先拉取文章內引用的 GitHub 儲存庫卡片資料 |
| `pnpm astro ...` | 執行原生 Astro CLI 指令（例如 `pnpm astro add`、`pnpm astro info`） |
| `pnpm astro --help` | 顯示 Astro CLI 完整說明文件 |

---

## 📝 文章創建與發布指南 (Posts)

### 1. 使用指令快速建立文章

透過 `pnpm new-post` 可自動在 `src/content/posts/` 下建立文章並填入當日日期與預設 Frontmatter（若檔名包含中文，腳本會自動將 `slug` 轉為拼音）：

```bash
# 在根目錄建立 src/content/posts/my-first-post.md
pnpm new-post my-first-post

# 支援多層子目錄分類，例如建立 src/content/posts/notes/astro-guide.md
pnpm new-post notes/astro-guide
```

### 2. 文章 Frontmatter 欄位說明

```yaml
---
title: 文章標題
published: 2026-10-28          # 發布日期 (必填)
updated: 2026-10-29            # 更新日期 (選填)
description: 文章摘要描述，會顯示於首頁文章卡片與 SEO Meta 中。
image: ./cover.webp            # 封面圖片路徑（支援相對路徑、public 路徑、外部 URL，或填 "api" 啟用隨機封面圖）
tags: [Astro, 筆記, 二次元]    # 文章標籤陣列
category: 技術筆記             # 文章分類
draft: false                   # 草稿模式：設為 true 時僅本地 pnpm dev 可見，正式建置會自動隱藏
pinned: false                  # 置頂文章：設為 true 時固定排列於首頁最上方
comment: true                  # 是否開啟留言區 (預設 true)
password: ""                   # 文章加密密碼：填入字串即啟用密碼保護 (選填)
passwordHint: ""               # 密碼提示文字 (選填)
series: ""                     # 系列文章名稱：相同 series 的文章會自動串聯成系列專欄 (選填)
seriesOrder: 1                 # 系列文章排序編號 (選填)
lang: ""                       # 僅當單篇文章語言與 siteConfig.ts 預設語言 (zh_TW) 不同時設定
author: ""                     # 自訂作者名稱（預設使用 profileConfig 設定）
sourceLink: ""                 # 轉載來源連結（若有填寫會於文末版權區塊顯示）
licenseName: ""                # 自訂單篇文章授權名稱 (選填)
licenseUrl: ""                 # 自訂單篇文章授權連結 (選填)
---
```

---

## 💬 動態創建與發布指南 (Dynamic)

動態檔案存放於 `src/content/dynamic/`，每個 `.md` 檔案代表一則隨手動態或短貼文。

### 1. 快速建立動態

```bash
# 使用短指令建立一則動態（自動以當前時間 YYYY-MM-DD-HHmmss.md 命名）
pnpm new-d 今天天氣真不錯，開始折騰新部落格！

# 或使用完整指令
pnpm new-dynamic 今天天氣真不錯，開始折騰新部落格！
```

### 2. 動態 Frontmatter 格式

```yaml
---
published: 2026-10-28 01:30:00
pinned: false      # 是否置頂該則動態 (選填)
location: Taipei   # 發布位置標籤 (選填)
---

這裡直接撰寫動態內容，完整支援 **Markdown** 語法與圖片插入。
```

> 💡 亦可於 [`src/config/dynamicConfig.ts`](src/config/dynamicConfig.ts) 中配置對接 [Memos](https://www.usememos.com/) 作為即時動態資料來源。

---

## 🧩 Markdown 擴充語法

除了標準 [GitHub Flavored Markdown (GFM)](https://github.github.com/gfm/) 外，部落格內建支援以下進階語法（可參考 `src/content/posts/` 下的範例文章）：

- **提示區塊 (Admonitions)**：支援 `:::note`、`:::tip`、`:::important`、`:::warning`、`:::caution` 以及 GitHub `> [!NOTE]` 語法。
- **GitHub 儲存庫卡片**：使用 `::github{repo="owner/repo"}` 嵌入動態資訊卡。
- **增強程式碼區塊 (Expressive Code)**：支援行號顯示、程式碼折疊 (`collapse={1-5}`)、標題列與一鍵複製。
- **數學公式與圖表**：內建支援 KaTeX 數學公式 (`$...$` / `$$...$$`)、Mermaid 流程圖與 PlantUML。

---

## 📖 專案目錄與配置結構

所有個人化設定均集中在 `src/config/` 目錄下，與程式碼邏輯分離，方便日後維護：

```text
src/
├── config/
│   ├── index.ts                  # 配置統一匯出索引
│   ├── siteConfig.ts             # 站點核心配置（標題、語言 zh_TW、Favicon、Logo、功能開關）
│   ├── backgroundWallpaper.ts    # 背景桌布配置（fullscreen 全螢幕毛玻璃 / banner 橫幅 / overlay 透明度）
│   ├── profileConfig.ts          # 個人資料卡配置（頭像、名稱 ゆうき、簽名、GitHub / RSS 連結）
│   ├── navBarConfig.ts           # 頂部導覽列連結與選單配置
│   ├── sidebarConfig.ts          # 側邊欄版面配置（單側欄 / 雙側欄、組件開關）
│   ├── coverImageConfig.ts       # 文章隨機封面圖與 API 配置
│   ├── displaySettingsConfig.ts  # 前台主題色與顯示設定面板配置
│   ├── dynamicConfig.ts          # 動態頁面與 Memos 串接配置
│   ├── effectsConfig.ts          # 頁面視覺特效配置（櫻花飄落、雪花等）
│   ├── expressiveCodeConfig.ts   # 程式碼高亮主題配置
│   ├── fontConfig.ts             # 全站字型配置
│   ├── FooterConfig.html         # 頁尾自訂 HTML 內容注入
│   ├── friendsConfig.ts          # 友情連結資料配置
│   ├── galleryConfig.ts          # 相簿頁面配置
│   ├── licenseConfig.ts          # 文章尾端 CC 授權條款配置
│   ├── mermaidConfig.ts          # Mermaid 圖表渲染配置
│   ├── musicConfig.ts            # 音樂播放器配置
│   ├── pioConfig.ts              # 看板娘 (Live2D / Spine) 配置
│   ├── plantumlConfig.ts         # PlantUML 圖表配置
│   ├── commentConfig.ts          # 留言系統配置 (Twikoo / Waline / Giscus 等)
│   ├── analyticsConfig.ts        # 網站流量統計分析配置
│   ├── announcementConfig.ts     # 首頁公告欄配置
│   └── sponsorConfig.ts          # 贊助配置（目前已於 siteConfig.ts 關閉）
├── content/
│   ├── posts/                    # 部落格文章 (.md / .mdx)
│   ├── dynamic/                  # 個人動態短貼文 (.md)
│   ├── projects/                 # 專案展示卡片 (.md / .mdx)
│   └── spec/                     # 獨立頁面內容（about.md 關於頁、friends.mdx 友鏈頁）
└── public/                       # 靜態資源（favicon.ico、桌布圖片、音樂等）
```

---

## 🚀 自動化部署工作流 (GitHub Actions)

1. **主要分支**：`main` 為唯一生產分支。
2. **自動發布**：每當推送 (`git push origin main`) 至 GitHub 時，[`.github/workflows/deploy.yml`](.github/workflows/deploy.yml) 會自動在雲端啟動 Node.js 24 + `pnpm` 環境執行 `pnpm build`，並將產物部署至 GitHub Pages（[https://shiroiyuki.github.io/](https://shiroiyuki.github.io/)）。

---

## 📝 致謝與授權

- 網站框架基於 [Astro](https://astro.build/) 建置，主題修改自 [CuteLeaf/Firefly](https://github.com/CuteLeaf/Firefly) 與 [saicaca/fuwari](https://github.com/saicaca/fuwari)（MIT License）。
