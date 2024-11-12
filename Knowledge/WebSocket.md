
WebSocket 是一種網路通訊協定，設計用來實現瀏覽器與伺服器之間的**雙向、持久連接**，允許兩者之間能夠在單一連接上進行**即時**的訊息交換。它是在 HTTP 協定之上建立的，透過特定的握手機制來建立連接，成功後即轉換為 WebSocket 通訊，以避免每次資料傳輸進行 HTTP 請求。
### WebSocket 的運作方式
---
1. **握手階段**: 起初，客戶端 (通常是瀏覽器) 會向伺服器發送一個 HTTP 請求，並在標頭中包含 `Upgrade: websocket` 。伺服器如果支援 WebSocket，會返回一個符合協議的應答，從而完成連接。
2. **雙向持續通訊**: 握手完成後，瀏覽器與伺服器之間的通訊從 HTTP 切換為 WebSocket。這使得雙方可以在不重新建立連接的情況下，隨時互相傳送訊息。
3. **即時資料更新**: WebSocket 允許伺服器主動推送訊息給客戶端，而不僅僅是回應客戶端的請求，這對於需要即時更新的應用（例如聊天室、遊戲、股票市場）尤其有用。
### WebSocket 的優點
---
- **低延遲**: 因為連接是持續的，所以相比 HTTP 頻繁的請求-回應模型，WebSocket 減少了延遲。
- **雙向通訊**: 允許伺服器和客戶端互相發送資料。
- **節省帶寬**: 由於無需每次發送時都帶有完整的 HTTP 標頭，能有效減少帶寬消耗。
### 使用範例
---
#### JavaScript
```javascript
const socket = new WebSocket('ws://example.com/socket');

// 當連接打開時
socket.onopen = function() {
  console.log('Connected');
  socket.send('Hello Server!');
};

// 當收到來自伺服器的訊息時
socket.onmessage = function(event) {
  console.log('Message from server ', event.data);
};

// 當連接關閉時
socket.onclose = function() {
  console.log('Disconnected');
};
```
#### Python
```shell
pip install websockets
```
```python
import asyncio
import websockets

async def connect():
    uri = "ws://example.com/socket"  # 這裡替換為你的 WebSocket URL
    async with websockets.connect(uri) as websocket:
        # 發送訊息到伺服器
        await websocket.send("Hello Server!")
        print("Message sent to the server")

        # 等待並接收來自伺服器的訊息
        response = await websocket.recv()
        print("Message from server:", response)

# 啟動 asyncio 事件循環並執行 connect
asyncio.run(connect())
```
> `websockets.connect(uri)` : 這行建立與伺服器的連接，`uri` 是 WebSocket 伺服器的網址。
> `await websocket.send("Hello Server!")` : 將訊息發送到伺服器。
> `await websocket.recv()` : 等待並接收伺服器返回的訊息。

