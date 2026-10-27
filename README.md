# ゆうき's Blog (shiroiyuki.github.io) ❄️

> 這裡是 **[ゆうき (shiroiyuki)](https://shiroiyuki.github.io/)** 的個人技術筆記與二次元隨筆部落格。

- 🌐 **正式站點**：[https://shiroiyuki.github.io/](https://shiroiyuki.github.io/)
- 🚀 **技術架構**：[Astro](https://astro.build/) + [Firefly](https://github.com/CuteLeaf/Firefly)
- 🎨 **視覺風格**：全螢幕二次元立繪壁紙、半透明毛玻璃卡片、白雪冰藍專屬圖標

---

## 本地開發與寫作指令

專案強制使用 `pnpm` 套件管理器：

```bash
# 安裝依賴套件
pnpm install

# 啟動本地開發伺服器（支援熱重載即時預覽）
pnpm dev

# 本地靜態生產建置
pnpm build

# 本地預覽生產產物
pnpm preview
```

---

## 寫作與發布工作流

1. **撰寫文章**：在 `src/content/posts/` 目錄下新增 Markdown (`.md`) 或 MDX (`.mdx`) 檔案。
2. **草稿機制**：若文章尚未完成，可在文件開頭的 Frontmatter 加上 `draft: true`，本地可預覽但線上部署時會自動略過。
3. **自動發布**：將變更推送到 `main` 分支後，GitHub Actions 會自動執行雲端建置並發布至 GitHub Pages，約 1 分鐘後正式網站自動更新。
