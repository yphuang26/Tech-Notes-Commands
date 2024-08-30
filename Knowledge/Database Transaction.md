
### 什麼是 Transaction?
- Transaction 是資料庫執行過程中的一個「邏輯單位」
	- 一組一連串對資料庫進行存取、讀取的行為
- 每個 transaction 有兩種可能的結局: 
	- 全部執行成功
	- 全部不執行 (只要其中一個行為失敗就全部回滾)
- Transaction 主要是解決需要<span style="color:rgb(0, 176, 80)">一起發生的事件</span>但<span style="color:rgb(0, 176, 80)">事件或事件的參與者不同時或不一致</span>的問題。
- Transaction 存在有兩個主要目的:
	- 遭遇失敗時的時光機，當 transaction 中有至少一個操作失敗時，整個 transaction 都會回滾(rollback)，回到進行 transaction 「之前」的狀態。
	- 獨立作業的守護者，解決資料庫不一致的問題，讓不同 transaction 可以獨立不受干擾。
### Transaction 常見指令
- START TRANSACTION：建立一個 transaction
- COMMIT：TRANSACTION 中的操作結束時進行 commit
- ROLLBACK：也就是上面提到的可以將交易回滾
##### Save Point 儲存點
- 可以在交易中插入儲存點 (save point)，有需要時可以 rollback 到儲存點，而不用 rollback 整個交易。
### Transaction 四大特性: ACID
- <span style="color:rgb(0, 176, 240)">Atomicity 原子性</span> : 把整個交易視為一個原子，是一個不可分割的邏輯單位
- <span style="color:rgb(0, 176, 240)">Consistency 一致性</span> : 交易前後保持一致性
- <span style="color:rgb(0, 176, 240)">Isolation 隔離性</span> : transaction 過程中不能被其他 transaction 影響
- <span style="color:rgb(0, 176, 240)">Durability 永久性</span> : 一旦資料修改完成，便永續存在，就算系統發生故障也不應該毀損

參考: [Database Transaction & ACID](https://oldmo860617.medium.com/database-transaction-acid-156a3b75845e)
