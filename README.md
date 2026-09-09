# VOOM Gallery - 個人影片牆

> 這是一個基於 GitHub Pages 的個人影片典藏與播放專案，靈感來自 LINE VOOM 的瀑布流體驗。

**線上瀏覽：** https://taison833.github.io/voom/

![VOOM Gallery V1.5](https://img.shields.io/badge/Version-V1.5%20FIXED-00d492?style=for-the-badge)
![Videos](https://img.shields.io/badge/Videos-627-8b5cf6?style=for-the-badge)
![CDN](https://img.shields.io/badge/CDN-jsDelivr%20%2B%20GitHub%20Raw-ff6200?style=for-the-badge)

## 📖 專案介紹

本專案不是單純的檔案備份，而是完整的 **前端影片牆播放器**。所有影片透過自製的 `index.html` 瀑布流播放器呈現，支援搜尋、自動備援、快取刷新。

- **627 支影片典藏** - 2024-2026 個人創作與收藏
- **真實檔名 + 自動備援 (V1.5)** - 自動抓取 GitHub API 真實檔名，優先使用 jsDelivr CDN，失敗自動切換到 GitHub Raw
- **純前端，無後端** - 單一 `index.html` 即可運作，部署於 GitHub Pages

## 🚀 技術架構

```
GitHub Repo (voom/)
├── index.html          # V1.5 播放器主程式 (React 瀑布流)
├── *.mp4               # 627 支影片 (hash 命名，原始檔名保留)
└── README.md           # 本文件
      ↓
GitHub API (api.github.com/repos/taison833/voom/contents)
      ↓
播放器載入
├── 1. 嘗試 jsDelivr CDN: cdn.jsdelivr.net/gh/taison833/voom@main/{file}
└── 2. 備援 GitHub Raw: raw.githubusercontent.com/taison833/voom/main/{file}
```

### 為什麼有自動備援？

- `raw.githubusercontent.com` 對 10MB+ 影片有時會限速/429
- `jsDelivr` 是全球 750+ 節點的免費 CDN，剛上傳的檔案需時間快取
- V1.5 會自動嘗試：CDN 失敗 → 1秒後切 Raw，確保播放成功率

## 📂 檔案結構

- 影片命名：`{hash}_{timestamp}.mp4` - 原始匯出命名，保留唯一性
- 單檔大小：2MB - 15MB，符合 GitHub 100MB 限制
- 總倉庫大小：約 3GB，符合 GitHub 5GB 硬限制，但已超過 1GB 軟限制，未來新影片將遷移至 R2

## 🛠️ 如何使用

1. 直接瀏覽：https://taison833.github.io/voom/
2. 搜尋：右上角輸入檔名關鍵字，例如 `a1b2c3`
3. 刷新 CDN 快取：若新上傳影片顯示 404，訪問 `https://purge.jsdelivr.net/gh/taison833/voom@main/{filename}`

## 🔮 未來規劃 (Roadmap)

由於 GitHub 建議單倉庫 <1GB，本專案 627 支後的新影片將採用 **B 方案**：

- **Cloudflare R2** 作為專業影片倉庫 (免費 10GB，無檔案大小限制)
- GitHub Pages 僅保留 `index.html` 播放器，影片來源改為 `https://pub-xxx.r2.dev/{file}`
- 這將解決 Pages 部署速度與 GitHub 儲存政策問題

## ⚠️ GitHub 使用聲明

本倉庫為 **個人作品集展示專案**，`index.html` 為核心程式碼，影片為專案展示內容，非單純檔案儲存。如超過 GitHub 建議用量，已規劃遷移至 R2，符合 GitHub 可接受使用政策。

## 📄 License

MIT - 播放器程式碼可自由使用，影片內容保留個人版權。

---

Built with ❤️ by @taison833 | VOOM Gallery V1.5 - 真實檔名 + 自動備援
