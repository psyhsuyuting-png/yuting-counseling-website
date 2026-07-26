# 不連接帳號的架站與文章後台操作指南

你會全程在自己的瀏覽器操作 GitHub、Pages CMS 與 Cloudflare；不必把帳號權限交給任何人。

## 第一階段：把網站放進 GitHub

1. 登入 GitHub。
2. 右上角按 `+` → `New repository`。
3. Repository name 填：`yuting-counseling-website`。
4. 建議先選 **Private**。Pages CMS 能否存取私有儲存庫，取決於你授予它的 GitHub App 權限。
5. 不要勾選 README、.gitignore 或 License，建立空白儲存庫。
6. 解壓縮本網站檔案包。
7. 在 GitHub 儲存庫頁面選 `uploading an existing file`。
8. 上傳解壓後資料夾內的所有檔案與資料夾，而不是上傳 ZIP 本身。
9. Commit message 可填：`建立網站與文章後台`，按 `Commit changes`。

若瀏覽器一次無法上傳完整資料夾，可安裝 GitHub Desktop，登入後選擇本機資料夾再 Publish repository。GitHub Desktop 可只操作這個網站專用儲存庫。

## 第二階段：啟用 Pages CMS

1. 前往 `https://app.pagescms.org/`。
2. 選擇使用 GitHub 登入。
3. GitHub 顯示授權頁時，優先選擇 **Only select repositories**。
4. 只勾選 `yuting-counseling-website`，不要開放所有儲存庫。
5. 登入 Pages CMS 後，選擇這個儲存庫與預設分支。
6. Pages CMS 會讀取根目錄的 `.pages.yml`，左側應出現「文章」。

如果沒有看到文章：

- 確認 `.pages.yml` 位於儲存庫最外層。
- 確認 GitHub App 獲准存取這個儲存庫。
- 重新載入 Pages CMS。

## 第三階段：發布網站到 Cloudflare Pages

1. 登入 Cloudflare Dashboard。
2. 進入 `Workers & Pages` → `Create` → `Pages` → `Connect to Git`。
3. Cloudflare 要求 GitHub 權限時，同樣選擇只授權 `yuting-counseling-website`。
4. 選擇該儲存庫。
5. 建置設定：
   - Framework preset：`None`
   - Build command：`python3 -m pip install -r requirements.txt && python3 scripts/build.py`
   - Build output directory：`dist`
6. 按 Deploy。
7. 完成後會得到類似 `專案名稱.pages.dev` 的公開網址。

之後每次 Pages CMS 儲存文章，GitHub 內容會更新，Cloudflare Pages 會自動重新建置與發布。

## 第四階段：在後台新增文章

1. 登入 `https://app.pagescms.org/`。
2. 選擇網站儲存庫 →「文章」。
3. 按新增文章。
4. 填寫：
   - 文章標題
   - 網址名稱：只能用小寫英文、數字、連字號，例如 `understanding-anxiety`
   - 發布日期
   - 文章分類
   - 文章摘要
   - 封面圖片與圖片說明
   - SEO 標題與描述（可以留白）
   - 文章正文
5. 尚未完成時，將「儲存為草稿」打開。
6. 要公開時，關閉「儲存為草稿」再儲存。
7. 等待 Cloudflare 自動部署，通常幾分鐘內更新。

## 草稿的重要限制

草稿不會出現在公開網站，但仍儲存在 GitHub 儲存庫中。因此：

- 儲存庫建議設為 Private。
- 草稿也不要包含個案資料或可識別資訊。
- 文章案例必須充分匿名化，並遵循專業倫理及取得必要同意。

## 撤銷權限

你可隨時到 GitHub：

`Settings` → `Applications` → `Installed GitHub Apps`／`Authorized OAuth Apps`

分別調整或撤銷 Pages CMS、Cloudflare 的存取權。撤銷後，公開網站仍可能維持最後一次部署內容，但後台與自動部署會停止，直到重新授權。

## 正式網域

網站穩定後再購買網域即可。在 Cloudflare Pages 的 Custom domains 中加入網域。綁定後，要把 `scripts/build.py` 的 `BASE_URL` 改成正式網址，讓 SEO canonical 與 sitemap 指向正確網域。
