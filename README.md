# 徐鈺婷諮商心理師網站＋文章後台

這份專案保留目前網站外觀，並加入：

- Pages CMS 文章管理後台
- Markdown 文章內容
- 封面圖片上傳
- 草稿／發布狀態
- 自動產生首頁文章卡片
- 文章列表與獨立文章頁
- 每篇文章 SEO 標題與描述
- sitemap.xml 與 robots.txt

## 隱私原則

這個儲存庫只適合存放「準備公開」的網站內容。請勿放入：

- 個案姓名、電話、Email
- 預約名單
- 諮商紀錄、評估資料
- 私人文件或未取得同意的照片
- 密碼、金鑰、身分證明文件

草稿雖不會顯示在建置後的網站上，但檔案仍會儲存在 GitHub 儲存庫中。若草稿內容敏感，請不要寫入此後台。

## 本機建置

```bash
python3 -m pip install -r requirements.txt
python3 scripts/build.py
```

輸出網站位於 `dist/`。

## Cloudflare Pages 建置設定

- Build command：`python3 -m pip install -r requirements.txt && python3 scripts/build.py`
- Build output directory：`dist`
- Root directory：留白

## 正式網域設定

取得正式網域後，將 `scripts/build.py` 裡的：

```python
BASE_URL = "https://example.com"
```

改成正式網址，例如：

```python
BASE_URL = "https://www.your-domain.com"
```

這會同步更新 canonical、sitemap 與 robots.txt。
