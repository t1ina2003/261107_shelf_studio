# 層架練習室 · Shelf Studio

用手機先試擺，再動手整理。以兩張真實層架照片作為場景，把物件獨立成可拖曳圖層，也能加入自己的相片。

## GitHub description

Mobile-first shelf planner: rearrange photo cutouts on real shelves, upload photos, remove simple backgrounds, manually crop objects, and save layouts locally.

中文：手機層架排列工具：真實照片物件拖曳、相片上傳、簡單背景自動去背、手動裁切與本機配置儲存。

## 功能

- 深灰層架、木色層架兩個場景；原始照片可切換對照。
- 29 個預設物件／收納組合，利用輪廓遮罩從原照擷取；被遮住的物件不會憑空重建，因此部分用品以組合保留。
- 手指拖曳、雙指縮放、大小滑桿、旋轉、層級調整、複製、刪除、跨層架移動。
- 靠近層板時對齊底緣，可關閉。
- 手機上傳照片、逐點多邊形裁切、橡皮擦、自動移除邊緣相近的背景。
- 自動去背景會移除與照片邊緣相近的顏色，適合單色背景。複雜背景可手動描邊。
- IndexedDB 自動儲存、35 步復原／重做、PNG 排列圖、JSON 備份匯入／匯出。
- 無後端、無 API key、無追蹤、無第三方執行時依賴。新增相片只在使用者的瀏覽器處理，並不提交至 GitHub。

## 執行

需要 Node.js 22+（檢查／測試）及 Python 3（本機伺服器）。網站本身是純靜態檔案。

```sh
npm run check
npm test
python -m http.server 8000
```

開啟本機 `http://localhost:8000`。手機測試時，可在相同 Wi-Fi 以電腦的區網 IP 存取伺服器。

## Git flow

本專案使用實際 Git 分支與 merge commit 保留發行歷程，不只建立空的分支名稱。

- `main`：正式發行，GitHub Pages 僅部署此分支。
- `develop`：下一版本整合。
- `feature/mobile-shelf-planner`：初版功能，完成後合併至 develop。
- `release/1.0.0`：發行準備，完成後合併至 main 並回合併 develop。
- 後續緊急修正由 `main` 建立 `hotfix/*`，完成後同時合併回 main 與 develop。

## GitHub Pages 發布

在 GitHub 的 Settings → Pages 將 Source 設為 **Deploy from a branch**，選擇 **main** 和 **/(root)**，再按 Save。網站是靜態檔案，`.nojekyll` 讓 GitHub Pages 直接提供原始檔案。

- [GitHub Pages 網址](https://t1ina2003.github.io/261107_shelf_studio/)
- [發布設定](https://github.com/t1ina2003/261107_shelf_studio/settings/pages)

## 資料與限制

- 空架底圖由提供的照片經 AI 移除物件並補繪，幾何可能略有差異。僅供視覺排列，不代表真實尺寸、層架承重或電器散熱間距。
- 每架最多 150 個物件，上傳相片上限 25 MB，會縮到最長邊 1200 px；備份上限 50 MB。
- 支援瀏覽器可解碼的格式，建議 JPG、PNG、WebP。部分瀏覽器無法直接解碼 HEIC，請先轉檔。
- 跨裝置以 JSON 備份移轉，沒有帳號或雲端同步。無痕模式及清除瀏覽資料可能移除配置。

## 素材

`assets/*-original.webp` 是使用者提供的照片（以 WebP 發布，已移除 EXIF metadata）。`assets/*-empty.webp` 是使用內建圖像生成工具所產生的空層架，提示要求移除全部物品、保留架體、視角與牆面。`presets.js` 定義原圖座標的裁切輪廓。原照片與品牌圖像不自動授予第三方再利用權利。
