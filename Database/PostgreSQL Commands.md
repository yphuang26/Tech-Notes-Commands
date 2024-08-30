
### Connect to remote PostgreSQL server
```shell
psql -h {ip_address} -U root -d mydb
```

PostgreSQL 是一個關連式資料庫管理系統（RDBMS）。這表示它是一個管理關連性質資料的系統。關連性，基本上在數學裡是以資料表（table）的形式來表現的。

#### 創建一個新的資料表
```sql
CREATE TABLE weather (
	city     varchar(80),
	temp_lo  int, --low temperature
	temp_hi  int, --high temperature
	prcp     real, --precipitation
	date     date
);
```
- 空白可以自由使用在 SQL 指令當中，psql 是以分號作為指令結束的判定。”—” 表示緊接的內容只是註解，值到該行結束為止。
- PostgreSQL 是不分大小寫字母的，包括各類關鍵字和描述語，除非是使用雙引號括起來的文字。
- varchar(80) 表示指定一個資料型別，它可以儲放任意 80 個字元以內的字串。
- PostgreSQL 支援標準的資料型別 int, smallint, real, double precision, char(N), varchar(N), date, time, timestamp, interval，也支援了複合型的地理資料型別。

```sql
-- point 型別是一個 PostgreSQL專屬資料型別的範例。
CREATE TABLE cities (
	name      varchar(80),
	location  point
);
```

```sql
DROP TABLE table_name;
```
#### 資料列
- 是資料表的組成單位
```sql
-- 需要依照欄位宣告的次序擺放# 需要依照欄位宣告的次序擺放
INSERT INTO weather VALUES ('San Francisco', 46, 50, 0.25, '1994-11-27');
-- or
-- 可以將欄位以不同的次序擺放，也可略去某些欄位
INSERT INTO weather (city, temp_lo, temp_hi, prcp, date)
	VALUES ('San Francisco', 43, 57, 0.0, '1994-11-29');
```

```sql
-- COPY 指令為了大量資料輸入而設計 (檔案必須存在於後端的伺服器中)。
COPY weather FROM '/home/user/weather.txt';
```
#### 資料表的查詢
```sql
SELECT * FROM weather;
# or
SELECT city, temp_lo, temp_hi, prcp, date FROM weather;
```

```sql
-- 可以在回傳列表中撰寫一些運算表示式
SELECT city, (temp_hi+temp_lo)/2 AS temp_avg, date FROM weather;
```

```sql
-- 查詢語句可以加上「WHERE」來設定限制條件，以指定哪些列才需要被回傳
SELECT * FROM weather
    WHERE city = 'San Francisco' AND prcp > 0.0;
```

```sql
-- 可以將結果進行排序
SELECT * FROM weather
    ORDER BY city;
```

```sql
-- 可以在查詢時去除重覆的列
SELECT DISTINCT city
    FROM weather;
```

#### 交叉查詢 (join)
- 在一個查詢之中，涉及到同一個或多個不同的資料表中的資料，稱作為交叉查詢（join）。
```sql
SELECT city, temp_lo, temp_hi, prcp, date, location
    FROM weather, cities
    WHERE city = name;
```

```sql
SELECT weather.city, weather.temp_lo, weather.temp_hi,
       weather.prcp, weather.date, cities.location
    FROM weather, cities
    WHERE cities.name = weather.city;
```

```sql
SELECT *
    FROM weather INNER JOIN cities ON (weather.city = cities.name);
```

#### 彙總查詢
- 彙總查詢指的是能夠把多個資料列的資料經過計算，產生單一結果的功能。舉例來說， count、sum、avg（平均值）、max（最大值）、min（最小值）都是彙總查詢的函式。
```sql
SELECT max(temp_lo) FROM weather;
```

```sql
SELECT city FROM weather
    WHERE temp_lo = (SELECT max(temp_lo) FROM weather);
```

```sql
-- 彙總查詢和 GROUP BY 一起使用會很方便的。舉例來說，我們可以得到每個城市所觀測到的最高氣溫
SELECT city, max(temp_lo)
    FROM weather
    GROUP BY city;
```

```sql
-- 我們可以進一步過濾資料內容，使用 HAVING
SELECT city, max(temp_lo)
    FROM weather
    GROUP BY city
    HAVING max(temp_lo) < 40;
```
#### 更新資料
```sql
UPDATE weather
    SET temp_hi = temp_hi - 2,  temp_lo = temp_lo - 2
    WHERE date > '1994-11-28';
```
#### 刪除資料
```sql
-- 刪除資料表中的特定資料
DELETE FROM weather WHERE city = 'Hayward';
```

```sql
-- 刪去資料表中的所有資料
DELETE FROM table_name;
```
