
開發的應用程式往往因為作業系統、環境變數等等，導致許多未知的問題。Docker 透過**容器技術**，將應用程式及其依賴的所有環境打包在一起，確保應用在任何環境下都能一致地執行。
1. 在作業系統上架設 Docker Engine
2. 將應用程式打包成「標準化單元」，在 Docker Engine 上運行
3.  ![[docker_engine.png|400]]
### Docker 重要觀念
**映像檔 (Image)**: 利用 Docker Engine 將「應用程式」打包的一個唯獨單元
**容器 (Container)**: 利用映像檔建立的一個執行實例 (runtime instance)，一個映像檔可建立多個容器
**倉庫 (Registry)**: 存放映像檔的地方，分為公用倉庫及私有倉庫