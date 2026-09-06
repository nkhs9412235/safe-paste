# Safe Paste

[English](README.md)

一個以隱私為優先、完全在瀏覽器端執行的機密資料遮蔽工具，讓你在分享終端機輸出或 Log 前，自動移除密碼、API Key、Token 與其他敏感資訊。

## 為什麼需要 Safe Paste？

將終端機輸出、Docker Log、設定檔或除錯資訊貼到 ChatGPT、Coding Agent、Issue Tracker 或團隊聊天室時，很容易在沒有注意到的情況下，把 API Key、Password、Token 或其他憑證一起貼出去。

Safe Paste 的目的，就是在「複製原始資料」與「分享出去」之間增加一道簡單的本機安全檢查。

## 功能

- 自動將常見 Password、API Key、Secret 與 Token 替換成 `***`
- 偵測 Authorization Bearer 與 Basic credentials
- 遮蔽資料庫與其他連線 URL 中的帳號密碼
- 辨識 OpenAI、GitHub、GitLab、Slack、Google、AWS、Stripe、JWT、Private Key 等常見憑證格式
- 對疑似未知 Secret 的高 entropy 字串顯示警告，而不是直接破壞可能有用的除錯資料
- 可選擇強化欄位偵測模式
- 一鍵複製清洗後內容
- 適合桌面與手機瀏覽器的響應式介面
- 自動支援淺色／深色模式
- 不需要 Backend

## 隱私設計

Safe Paste 的文字處理完全在你的瀏覽器內進行。

目前實作不會刻意將貼上的內容傳送到伺服器，也不會寫入 `localStorage`、Cookie 或 IndexedDB。整個應用程式是一個純靜態 HTML 頁面，不需要 API 或後端服務。

若處理高度敏感資料，仍建議自行檢查原始碼以及實際部署環境後再使用。

## 使用方式

1. 在瀏覽器開啟 Safe Paste。
2. 將終端機輸出、Log、設定檔或其他文字貼入輸入框。
3. Safe Paste 會自動掃描並遮蔽已知格式的機密資料。
4. 如果出現黃色警告，人工確認無法安全分類的疑似機密字串。
5. 按下「複製安全內容」，再將清洗後的結果貼到 ChatGPT、Coding Agent 或其他地方。

輸入範例：

```text
password="hello123"
OPENAI_API_KEY=sk-example-secret-value
Authorization: Bearer example-token-value
DATABASE_URL=postgresql://user:password@localhost/db
```

處理結果：

```text
password="***"
OPENAI_API_KEY=***
Authorization: Bearer ***
DATABASE_URL=postgresql://user:***@localhost/db
```

## 本機執行

Safe Paste 不需要編譯，也沒有套件相依性。Clone repository 後直接用現代瀏覽器開啟 `index.html` 即可。

```bash
git clone https://github.com/nkhs9412235/safe-paste.git
cd safe-paste
open index.html
```

不同瀏覽器對 Clipboard API 有不同的安全限制。若直接開啟本機 HTML 時無法使用剪貼簿功能，可以透過本機 HTTP Server 提供頁面，以取得較一致的剪貼簿支援。

## 重要限制

Secret 偵測本質上屬於啟發式判斷。任何 Regex 或 entropy-based scanner 都無法保證辨識所有自訂格式的機密資料。

因此 Safe Paste 應視為「分享資料前的額外安全層」，而不是完整的 DLP（Data Loss Prevention）或 Secret Management 系統。

## 授權

目前尚未指定 License。
