
要讓裝有 Web Server 的 EC2 連入到裝有 PostgreSQL Server 的 EC2

**停止執行個體 IP 地址會改變（下面內容需重新設定）**

1. Database server 安全群組的傳入規則增加 Web server
2. 修改 Database server 的 pg_hba.conf (/etc/postgresql/{version}/main/pg_hba.conf)
3. MySQL 或 PostgreSQL client 連入

#### Additional notes:
**Inbound**: 伺服器對外開放的部分
**Outbound**: 伺服器可否對外連線部分，通常不會限制