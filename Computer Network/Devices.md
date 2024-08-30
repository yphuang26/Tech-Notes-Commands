
- <span style="color:rgb(0, 176, 80)">Modem (modulator-demodulator，數據機)</span>: Used to connect to the Internet.
- <span style="color:rgb(0, 176, 80)">Router (路由器)</span>: Acts as a gateway to the computer network and is placed between a modem and a switch or hub.
	- IP 分享器，提供多個不同的 IP 給後端設備上網使用
	- Wi-Fi 分享器可以額外透過無線訊號 (Wi-Fi) 分享 IP，讓手機或其他無線設備達上網的功能
	- 路由器的網路孔分成對外 (WAN) 和對內 (LAN):
		- WAN 端要接網路業者的訊號線或是數據機，連到外部網際網路
		- LAN 端則是要接家中要連線上網的設備，例如電腦或電視都是內網
- <span style="color:rgb(0, 176, 80)">Switch (交換器)</span>: Connects devices such as desktop, laptop, and access point to the router.
	- 交換器可以讓連線設備形成區域網路 (內網)，所有的孔都是 LAN 端，交換器會記錄電腦的 MAC (網卡) 位址，每一台的網卡都不相同，封包能傳給指定的對象
	- 常拿來當作分享器的線路擴充，但交換器不會主動配發 IP，必須由前端的分享器或數據機配發，一對多提供 IP 位址給後端多台接線上網的電腦或其他設備
	- 使用情境:
		- 如果分享器的 LAN 孔不夠使用，可以準備一台交換器接在分享器的 LAN 端，透過交換器就能再多接幾台設備
		- 常見的應用有電腦連線印表機、不同電腦的共用資料夾或是手機投放畫面到電視觀看 (使用 Wi-Fi 連線也是能達到相同內網的效果)
- <span style="color:rgb(0, 176, 80)">Access Point (AP，存取點)</span>: Connects a device wirelessly.
	- 存取點是區域網路 (LAN) 內的設備，用於擴展電腦網路的無線覆蓋範圍。 這可以增加可以連接到電腦網路的使用者數量


![[computer_network.png|550]]


**MAC 位址 (Media Access Control Address)**
- MAC 地址是網路設備（例如電腦、手機、路由器等）的唯一識別符號。它是由網絡接口卡（NIC）或網絡接口控制器（NIC）固化在硬件中的一個 48 位元的十六進位數字組成，通常以冒號分隔（例如 00:1A:2B:3C:4D:5E）。MAC 地址可以想像成網絡裝置的 "身份證"。
**LAN IP 位址 (Local Area Network IP Address)**
- LAN IP 是在局域網（Local Area Network）內部分配給裝置的 IP 地址。這個 IP 位址通常是由路由器（或其他網絡設備）自動分配，用於在同一個局域網中的裝置之間通訊。它是在 RFC 1918 中定義的私有 IP 地址範圍之一，例如 192.168.x.x、172.16.x.x 至 172.31.x.x 和 10.x.x.x。
**WAN IP 位址 (Wide Area Network IP Address)**
- WAN IP 是分配給路由器或網絡設備連接到互聯網的 IP 地址。這是路由器在互聯網上的識別符號，用於與其他遠端網絡設備通訊。WAN IP 通常由網絡服務提供商（ISP）分配，可以是靜態 IP 地址（固定不變）或動態 IP 地址（可能會在連接重新建立時更改）。

總的來說，MAC 地址是裝置的硬件識別符號，而 LAN IP 地址和 WAN IP 地址則是用於在局域網和廣域網中進行通訊的網絡位址。

