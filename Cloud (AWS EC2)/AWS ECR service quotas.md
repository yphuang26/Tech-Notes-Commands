**查看目前 Amazon ECR 的 Service Quotas 設定**: 搜尋並選擇「Service Quotas」服務 -> 在左側導航欄中，選擇 「AWS Services」(AWS 服務) -> 在出現的服務列表中，搜尋並選擇「Amazon Elastic Container Registry (Amazon ECR)」
### BatchGetImage
---
**功能**：`BatchGetImage` 是一個 API 操作，允許一次性獲取多個 Docker 映像的指定標籤或摘要。這個操作會返回一個或多個映像的元數據和層的具體內容。
**具體使用場景**：當需要從 ECR 中提取多個映像以部署或分析時，可能會使用這個 API。每次調用這個 API，可以同時獲取多個映像，而不是一個一個單獨請求，這樣可以提高效率。
**配額限制**：此配額限制每秒可以使用 `BatchGetImage` 操作的最大次數。這是為了防止過多的同時請求對系統造成壓力。當超出這個限制時，可能會遇到 API 請求的限流（throttling）。
### GetDownloadUrlForLayer
---
**功能**：`GetDownloadUrlForLayer` 是一個 API 操作，用於獲取 Docker 映像層的下載 URL。每個 Docker 映像由多個層（layers）組成，這些層是二進制文件，表示應用程序的不同部分。這個 API 會為指定的層生成一個臨時的下載 URL，供直接下載這些層。
**具體使用場景**：當拉取（pull）一個映像時，ECR 會使用這個 API 來提供每個層的下載 URL。這樣，Docker 客戶端可以並行地下載各個層，加快整個拉取過程。
**配額限制**：此配額限制每秒可以請求的下載 URL 次數。如果這個配額被觸發，可能會導致下載過程變慢，甚至出現請求被限流的情況。
### GetAuthorizationToken
---
**功能**：`GetAuthorizationToken` 是一個 API 操作，返回一個 Base64 編碼的授權令牌，這個令牌用於認證 Docker 客戶端對 ECR 的訪問。授權令牌包括帳戶名稱和密碼，並且有效期有限。
**具體使用場景**：當 Docker 客戶端需要從 ECR 拉取或推送映像時，需要先進行身份驗證。通常，這個 API 是在第一次登錄 ECR 或者當前授權令牌過期時使用的。授權令牌會被 Docker 用於後續的 API 調用。
**配額限制**：此配額限制每秒可以生成的授權令牌次數。過多的請求可能會導致授權過程變慢或請求被拒絕，尤其在大量分布式系統中頻繁進行認證時可能會遇到這種情況。
### CompleteLayerUpload
---
**功能**：`CompleteLayerUpload` 是一個 API 操作，用於告知 ECR 某個 Docker 層的上傳已經完成。在成功上傳層後，需要調用這個 API 來完成上傳，並將該層標記為可用。
**具體使用場景**：在推送（push）一個 Docker 映像到 ECR 時，每個層都需要分別上傳。當所有層都成功上傳後，必須調用 `CompleteLayerUpload` 來確認這個層的上傳並完成這個過程。如果沒有調用這個 API，ECR 不會將這個層視為可用，從而導致映像無法完整使用。
**配額限制**：此配額限制每秒可以完成層上傳的次數。這個配額防止系統被過多的上傳操作淹沒，如果這個限制被超過，可能會發現上傳過程受到限制。