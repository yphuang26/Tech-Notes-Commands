
開發的應用程式往往因為作業系統、環境變數等等，導致許多未知的問題。Docker 透過**容器技術**，將應用程式及其依賴的所有環境打包在一起，確保應用在任何環境下都能一致地執行。
1. 在作業系統上架設 Docker Engine
2. 將應用程式打包成「標準化單元」，在 Docker Engine 上運行
3.  ![[docker_engine.png|400]]
### Docker 重要觀念
---
**映像檔 (Image)**: 利用 Docker Engine 將「應用程式」打包的一個唯獨單元
**容器 (Container)**: 利用映像檔建立的一個執行實例 (runtime instance)，一個映像檔可建立多個容器
**倉庫 (Registry)**: 存放映像檔的地方，分為公用倉庫及私有倉庫
### Docker 原理
---
##### Docker 與 Virtual Machine 的差別
**虛擬機 (Virtual Machine)**: 是在作業系統層級進行虛擬化，在主機作業系統上建立獨立的客體作業系統環境 (Guest OS)。
**Docker**: 是在應用程式層級進行虛擬化，將應用程式及其相依的函式庫、配置檔打包成映像檔(Image)，共用主機作業系統。
##### Docker 共用 Linux 核心模組
---
Docker 容器並不模擬完整的硬體環境，而是運行在主機的作業系統上。
Docker 利用 Linux 的**命名空間 (Namespaces)** 和**控制組 (Cgroups)** 來實現容器的隔離和資源管理。Namespace 提供了進程隔離，使得每個容器在自己的環境中運行，無法直接訪問其他容器的資源。Cproup 則限制了容器使用的資源 (如 CPU 和記憶體)，確保資源的有效分配。
### Docker Layer
---
每個 Docker 映像由多個層組成，這些層是 Read-Only 的，每一層代表一組檔案系統的變更 (如新增、刪除或修改)。當在 Dockerfile 中指定指令時 (例如 `FROM` 、`RUN` 、`COPY` 、`ADD` 等)，每個指令都會創建一個新的層。這些層是通過聯合檔案系統 (Union File System) 堆疊在一起，形成一個完整的映象。
##### Layer 的特性
**可重用性**: 如果多個應用程序基於相同的基礎映像，Docker可以重用這些層，而無需重複下載或構建。
**Layer 的緩存**: Docker使用層的緩存機制來加速映像的構建過程。如果某一層未發生變化，Docker會重用該層，這意味著在修改Dockerfile時，只有變更的層及其之上的層會被重新構建。這樣可以顯著減少構建時間。
**Layer 的不可變性**: Docker層是不可變的，這意味著對層的任何更改都會導致創建一個新的層。這種特性使得版本控制和回滾操作變得簡單，因為每個層都代表了一個特定的狀態。
##### Layer 的建構範例
---
撰寫 Dockerfile 時，每一行指令都會生成一個新的 Layer:
```sh
FROM ubuntu:20.04
RUN apt-get update && apt-get install -y python3
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
CMD ["python3", "app.py"]
```
在這個例子中，將會生成五個層:
- 基礎映像層 (Ubuntu)
- 更新和安裝 Python 的層
- 複製應用程式檔案的層
- 設定工作目錄的層
- 安裝依賴的層
