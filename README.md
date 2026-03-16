# 使用 Claude Code 探索與開發專案
### 下載 'initial' 分支的壓縮檔
https://github.com/uopsdod/claude_code_treasure_game/tree/initial

### 初始化上下文
/clear
/init: 生成 CLAUDE.md 以了解此專案的運作方式

npm install
npm run dev'

### 將檔案加入當前上下文
> 使用 @src/audios/chest_open.mp3 在 @src/App.tsx 中播放開啟寶箱的音效。不要做其他任何事情。

### 增加更多上下文
> 查看現有變更的註解

先輸入 '#'
「在每個新函式頂部加上一行單行註解，說明其用途，並且必須記錄輸入與輸出參數」
> 2. 專案記憶

> 使用 @src/audios/chest_open_with_evil_laugh.mp3 在 @src/App.tsx 中播放開啟含骷髏頭寶箱的音效

> 查看現有變更的註解

### 使用截圖直觀開發
> 截圖並標記你想要變更的區域。
> [!image] 根據最終分數，在圈選處顯示結果：勝利、平局或失敗

### 挑戰：更改滑鼠游標懸停圖示
當滑鼠懸停在已關閉的寶箱上時，使用 src/assets/key.png 圖示

### 管理上下文
/context
54k/200k tokens (27%)

> （選用）遞迴瀏覽該網址，了解 SQLite 的所有資訊並將內容加入上下文。
https://nodejs.org/docs/latest/api/sqlite.html

/compact

/context
> 26k/200k tokens (13%)

/clear

/context
> 16k/200k tokens (8%)

> 「檢查我的 AngularJS 專案是否有語法錯誤。」

esc + esc > 選擇一個對話以返回

### 計畫模式：
建立一個 commit 以儲存目前狀態

shift + tab
> 「我有哪些資料庫選項可以實作註冊與登入流程？」
> 「SQLite 作為本地儲存如何？」
> 「使用 SQLite 建立簡單的註冊與登入流程，並為每個已登入的使用者儲存遊戲分數。此外，允許以訪客模式進行遊戲而不儲存任何資料。」

> Ctrl + T：查看待辦事項清單

### 超深度思考（Ultrathink）
恢復至先前的 git commit

> 「超深度思考：使用 SQLite 建立簡單的註冊與登入流程，並為每個已登入的使用者儲存遊戲分數。此外，允許以訪客模式進行遊戲而不儲存任何資料。」

> Ctrl + T：查看待辦事項清單

### 自訂指令 - Vercel 部署
- 建立資料夾：.claude/commands
- 建立檔案：deploy_vercel.md
- 建立後，重新開啟一個新的 Claude Code 工作階段

### 自訂指令 - GitHub Pages 部署
- 建立資料夾：.claude/commands
- 建立檔案：deploy_github_page.md
- 建立後，重新開啟一個新的 Claude Code 工作階段
