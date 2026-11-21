# 資料結構專題

本專案使用 C 語言開發，並透過 Docker 建立一致的編譯環境。以下步驟以 Windows PowerShell 為例；Git 指令也可在 Git Bash 或 macOS/Linux 終端機使用。

---

## 開發環境

### 準備工具

請先安裝並啟動 Docker Desktop，並安裝 Git。第一次使用 Git 時，請設定提交時要顯示的姓名與 Email：

```bash
git config --global user.name "你的姓名"
git config --global user.email "你的Email"
```

### 建立 Docker 映像檔

在專案根目錄（有 `Dockerfile` 的資料夾）執行。第一次使用，或 Dockerfile／開發環境依賴有變更時才需要重新建立：

```bash
docker build -t c-env .
```

### 啟動環境

在專案根目錄執行以下指令，將電腦上的 `src` 資料夾掛載到容器的 `/app`：

```powershell
docker run --rm -it -v "${PWD}/src:/app" c-env
```

看到容器的命令提示字元後，以下指令都在容器內執行。

### 編譯與執行

```bash
make run
```

只執行已編譯的程式：

```bash
./main
```

清除編譯產生的執行檔：

```bash
make clean
```

輸入 `exit` 可離開容器。容器使用 `--rm`，離開後容器會自動移除；修改過的程式仍會保留在電腦的 `src` 資料夾。

---

## Git 與 GitHub 協作

### 1. 第一次下載專案

在 PowerShell 切換到想放專案的資料夾後，執行：

```bash
git clone https://github.com/4brams/Data_Structure_Project.git
cd Data_Structure_Project
```

`clone` 只需執行一次。若 GitHub 要求登入或授權，依畫面指示使用瀏覽器完成；不要把密碼或 Token 貼到程式碼或提交記錄中。

### 2. 開始工作前更新主要分支

每次開始新工作前，先切回主要分支並下載最新版本：

```bash
git checkout main
git pull origin main
```

### 3. 建立自己的分支

不要直接在 `main` 上修改。每個功能或修正都建立一個新分支。

```bash
git checkout -b 分支名稱
```

分支名稱格式 `你的名字-新功能簡述`例如 `abrams-hireFarmTools`

確定分支有建立、切過去：

```bash
git branch
```

### 4. 提交更新（commit）

先查看有哪些檔案被修改：

```bash
git status
```

確定目前自己在要提交的分支上：

```bash
git branch
```

將要提交的檔案加入暫存區：

```bash
git add 檔案路徑
```

例如：

```bash
git add src/main.c
```

或一次加入全部檔案：

```bash
git add *
```

接著建立提交，訊息要簡短說明這次做了什麼：

```bash
git commit -m "Commit訊息"
```

Commit訊息格式：

- `add`：新增功能，例如`add: yanghao to farm`
- `update`：更新功能，例如`update: plant new crops`
- `fix`：修bug，例如`fix: retaking calculus`
- `chore`：與主專案無關的更新，例如`chore: whipping yanghao`

尚未完成的修改可以分多次 commit；commit 只會記錄在本機，還沒有送到 GitHub。

### 5. Push 分支到 GitHub

第一次推送這個分支時執行：

```bash
git push -u origin 分支名稱
```

之後在同一分支有新的 commit，只需執行：

```bash
git push
```

`push` 會把分支和提交上傳到 GitHub，但不會直接合併到 `main`。

### 6. 在 GitHub 建立 Pull Request

1. 開啟專案的 GitHub 頁面：<https://github.com/4brams/Data_Structure_Project>。
2. Push 完成後，頁面通常會出現 **Compare & pull request**；點選它。若沒有出現，前往 **Pull requests** → **New pull request**。
3. 確認 **base** 是要合併進去的主要分支（通常是 `main`），**compare** 是自己的工作分支。
4. 填寫標題和說明（簡單寫）。
5. 按 **Create pull request**，等我按同意。

PR 建立後若還要修改，回到同一個分支修改、`git add`、`git commit`、`git push`；新提交會自動出現在同一個 PR，不必再開一個。

### 7. 檢查與合併

PR 合併完成後，回到本機更新主要分支：

```bash
git checkout main
git pull origin main
```

接著為下一項工作建立新的分支。
