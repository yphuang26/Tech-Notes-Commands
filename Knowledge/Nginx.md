
### Nginx
Nginx (pronounced "engine x") is a **Web Server** that can also be used as a **Reverse Proxy**, **Load Balancer**, mail proxy and HTTP cache.

[網頁 HTTP 伺服器 Apache 與 Nginx 的優缺點比較](https://por.tw/Website_Design/%E7%B6%B2%E9%A0%81-http-%E4%BC%BA%E6%9C%8D%E5%99%A8-apache-%E8%88%87-nginx-%E7%9A%84%E5%84%AA%E7%BC%BA%E9%BB%9E%E6%AF%94%E8%BC%83%EF%BC%88%E7%B6%B2%E7%AB%99%E6%9E%B6%E8%A8%AD%E6%95%99%E5%AD%B8/)

#### Web Server
A web server is **computer software** and underlying hardware that accepts requests via **HTTP** (the **netwrok protocol** created to distribute web content) or its secure variant HTTPS.
A user agent (usually a **web browser** or **web crawler**) initiates communication by requesting a web page or other resource using HTTP, and the server responds with the content of the resource or an error message.

#### Reverse Porxy (反向代理)
Reverse Proxy 在電腦網路中是代理伺服器的一種。伺服器根據客戶端的請求，從其關聯的一組或多組後端伺服器 (如 Web 伺服器) 上取得資源，然後再將這些資源返回給客戶端，<span style="color:rgb(0, 176, 240)">客戶端只會得知反向代理的 IP 位址</span>，而不知道在代理伺服器後面的伺服器叢集的存在。
與前向代理不同，前向代理作為客戶端的代理，將從網際網路上取得的資源返回給一個或多個的客戶端，伺服器端（如Web伺服器）只知道代理的IP位址而不知道客戶端的IP位址。

![[forward_and_reverse_proxy.png]]

#### Load Balancer (負載平衡器)
In computing, load balancing is the process of distributing a set of tasks over a set of resources (computing units), with the aim of making their overall processing more efficient. Load balancing can optimize response time and avoid unevenly overloading some compute nodes while other compute nodes are left idle.

![[load_balancer.png]]

#### Web Cache (HTTP Cache)
Web 快取 (或 HTTP 快取) 是用於臨時儲存 (快取) Web 文件 (如 HTML 頁面和圖像)，以減少伺服器延遲的一種資訊科技。
Web 快取可以用於各種系統 (從 Web 內容的傳輸方向來看):
- **前向位置系統 (接受者或客戶端)**: 是Web伺服器網路外部的快取，例如在客戶電腦、ISP或公司網路上。網路感知前向快取就像一個前向快取，但只快取大量訪問的專案。客戶端（如網頁瀏覽器）也可以儲存網路內容以供重用。
- **反向位置系統 (內容提供者或Web伺服器端)**: 反向快取位於一個或多個Web伺服器和Web應用的前端，加速來自網際網路的請求，從而減少Web伺服器的高峰負載。搜尋引擎也可能會快取一個網站，例如 Google，Google搜尋結果中可以找到快取內容的連結。

[Web Cache (Wikipedia)](https://en.wikipedia.org/wiki/Web_cache)
