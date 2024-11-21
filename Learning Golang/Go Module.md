
`go mod` 是 Go 編程語言用來管理依賴和模組的工具，它是 Go Modules 的一部分。Go Modules 是自 Go 1.11 引入的一個依賴管理系統，用於解決大型應用程式和開源庫中依賴的管理問題。
### `go mod` 基本概念
---
#### 1. 模組 (Module)
- 一個模組是由一組相關的 Go 程式文件和其依賴組成的。
- 模組由一個 `go.mod` 文件描述，這個文件定義了模組的名稱和它的依賴。
#### 2. `go.mod` 文件
- 這是模組的核心文件，記錄了模組的名稱和版本化的依賴。
- 格式範例:
```go
module example.com/mymodule

go 1.20

require (
    github.com/sirupsen/logrus v1.9.0
    golang.org/x/net v0.5.0
)
```
#### 3. 模組版本
- Go Modules 使用語義化版本控制（SemVer）來指定依賴的版本，例如 `v1.2.3`。
- 可以鎖定或升級到某個特定版本。
### 常用命令
---
#### 1. 初始化模組: `go mod init`
- 在專案目錄下執行，創建一個新的 `go.mod` 文件，並設置模組名稱。
```bash
go mod init example.com/mymodule
```
#### 2. 下載依賴: `go mod tidy`
- 下載專案所需但尚未下載的依賴，並移除未使用的依賴。
```bash
go mod tidy
```
#### 3. 更新依賴: `go get`
- 更新模組依賴的版本。
```bash
go get github.com/example/package@v1.2.3
```
- 如果不指定版本，默認會獲取最新的穩定版本。
#### 4. 檢查依賴: `go list -m all`
- 列出當前模組的所有依賴及其版本。
#### 5. 驗證依賴: `go mod verify`
- 驗證依賴是否被篡改或是否下載完整。
#### 6. 清理: `go mod vendor`
- 將所有依賴下載到專案的 `vendor` 資料夾中，適用於需要離線構建的場景。
### 工作流程
---
1. 初始化模組：`go mod init ${module-name}`。
2. 撰寫程式碼並引用第三方庫。
3. 使用 `go build` 或 `go run` 時，自動下載需要的依賴。
4. 使用 `go mod tidy` 確保 `go.mod` 和 `go.sum` 文件的依賴正確且清晰。
### 重要文件
---
1. `go.mod` : 描述模組和依賴。
2. `go.sum` : 記錄所有下載依賴的校驗和，確保依賴版本一致性。
