# 台灣知識種子計劃粉專成效追蹤

台灣知識種子計劃粉專成效追蹤，用於定期追蹤
[台灣知識種子計劃粉專](https://www.facebook.com/WSOTK)的貼文成效數據。

本系統以 Google Apps Script 撰寫，綁定於 Google Spreadsheet
上運行，透過 Facebook Graph API
自動抓取貼文的按讚數、留言數、分享數與觸及人數，並以週為單位持續追蹤變化。


## 功能特色

- 每週自動抓取粉專貼文數據（按讚、留言、分享、觸及人數）
- 每篇貼文持續追蹤 6 週（可自訂），觀察成效趨勢
- 按發文月份自動建立工作表分頁管理
- 統計日期統一對齊至週一，確保數據一致性


## 工作表結構

### 設定分頁

存放系統參數：

| 設定項目 | 說明 |
|---------|------|
| Access Token | Facebook Graph API 存取權杖 |
| 粉專 ID | Facebook 粉絲專頁 ID |
| 追蹤週數 | 每篇貼文追蹤幾週（預設 6 週） |
| 執行頻率 | 每週一早上 9:00 |
| 最後執行時間 | 系統自動更新 |

### 月份分頁（如 2026-01）

每篇貼文佔固定 6 行（對應 6 週追蹤）：

| 欄位 | 說明 |
|------|------|
| 貼文編號 | Facebook 貼文 ID（隱藏欄） |
| 發文時間 | 貼文發布時間（合併儲存格） |
| 貼文文字 | 貼文內容（合併儲存格） |
| 追蹤週次 | 第 1 週～第 6 週 |
| 統計日期 | 該週次對應的週一日期 |
| 按讚數 | 累計按讚數 |
| 留言數 | 累計留言數 |
| 分享數 | 累計分享數 |
| 觸及人數 | 不重複觸及人數 |


## 安裝與設定

1. 安裝相依套件：
   ```bash
   npm install
   ```
2. 登入 Google 帳號：
   ```bash
   npx clasp login --no-localhost
   ```
3. 建立一個新的 Google Spreadsheet，開啟「擴充功能」→「Apps Script」，
   從「專案設定」頁面複製 Script ID。
4. 複製 `.clasp.json.example` 為 `.clasp.json`，填入 Script ID：
   ```bash
   cp .clasp.json.example .clasp.json
   ```
5. 將程式碼推送到 Google Apps Script：
   ```bash
   npx clasp push
   ```
6. 在 Apps Script 編輯器中執行 `fetchAndUpdatePosts()` 函數，
   系統會自動建立「設定」工作表。
7. 在「設定」工作表中填入：
   - **Access Token**：從 [Facebook Graph API Explorer](https://developers.facebook.com/tools/explorer/) 取得
   - **粉專 ID**：Facebook 粉絲專頁的 ID
   - **追蹤週數**：每篇貼文要追蹤幾週（預設 6）
8. 執行 `setupWeeklyTrigger()` 設定每週一自動執行。


## 使用方式

- **自動執行**：設定觸發器後，每週一早上 9:00 自動執行。
- **手動執行**：在 Apps Script 編輯器中執行 `testRun()` 函數。
- **部署更新**：修改本地程式碼後，執行 `npx clasp push` 推送到 Google Apps Script。


## 授權條款

Copyright (c) 2026 imacat

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

<http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


## 作者

依瑪貓  
imacat@wikimedia.tw  
2026/2/14
