# VPS 比較：搞懂線路與機房的取捨順序，附 DMIT 洛杉磯／香港／東京全方案價格對照表

比較 VPS 的時候，最容易走偏的一步是盯著「2 核 4G」這類硬體數字比大小。同一組規格，一台在香港走三網 CN2 GIA、一台在美國走普通 163 回程，晚上八點之後的體驗差距，通常比 2 核換成 4 核明顯得多。

所以這篇不按「十大 VPS 排行」的寫法排，而是把比較的順序拆開：先確認你要服務誰，再看線路，再看機房與計費規則，最後才回到規格與價格。文末用 DMIT 目前的三條產品線做一份完整對照，讓你手上有一組具體數字可以比。

## 比較之前，先回答三個問題

1. **訪客在哪裡。** 面向中國大陸用戶、面向日本本地、還是面向歐美，答案完全不同。
2. **對延遲的容忍度。** 一般部落格與企業官網，120ms 和 40ms 對讀者的差別沒那麼大；但遠端桌面、遊戲連線、API 服務、支付回呼，這個差距會直接影響能不能用。
3. **月流量的底線。** 是 500GB 還是 5TB，決定你要不要為了省錢去挑「超量限速不斷線」的方案。

這三題答完，候選名單通常會從二十家縮到三、四家。

## 維度一：回程線路比硬體型號重要

去程是資料從你的網路出去，回程是資料從伺服器回來。台灣、香港、大陸的自架站站長真正在意的是回程，因為回程才是決定「打開網頁要等幾秒」的那一段。同一台機器，回程線路不同，晚高峰表現可以差一個等級。

幾條常見線路的實際定位：

| 線路 | 主要受惠的營運商 | 公開測評常見的國內延遲區間 | 晚高峰表現 | 價格級別 |
| --- | --- | --- | --- | --- |
| CN2 GIA（AS4809） | 電信最優，聯通次之 | 香港約 10–40ms、東京約 40–80ms、美西約 130–160ms | 丟包通常壓在 1% 以內，波動小 | 高 |
| CMIN2 / CMI | 移動為主 | 美西約 150ms 上下 | 移動用戶穩定，其他營運商視機房而異 | 中 |
| AS9929 / CUII | 聯通 | 美西約 150–180ms | 聯通表現好，其餘中等 | 中 |
| 國際 BGP／Tier 1 | 三者皆一般 | 美西 180–220ms，繞路時更高 | 高峰可能明顯掉速 | 低 |

上面這些數字是多家測評文章的常見區間，不是保證值。真正的判斷方式是向商家要測試 IP，自己在晚上八點到十一點跑一次 ping 與 traceroute，看回程是不是全程走在同一條優質 AS 上。很多標榜「CN2」的方案其實只有去程走 CN2，回程走 163，這種混搭線路白天好看，晚上現形。

## 維度二：機房位置是一道物理題

| 機房 | 對大陸訪客的常見延遲 | 線路選擇 | 價格印象 | 適合場景 |
| --- | --- | --- | --- | --- |
| 香港 | 10–40ms，幾乎與國內無感 | CN2 GIA、CMI、AS9929 都有 | 同規格最貴，頻寬最貴 | 面向大陸用戶的電商、企業站、低延遲應用 |
| 東京 | 約 40–80ms | 主要看軟銀、IIJ、CN2 GIA | 中等，同價位配置優於香港 | 日韓與東南亞業務、需要日本 IP 的場景 |
| 洛杉磯 | 約 130–180ms（優化線路） | CN2 GIA、CMIN2、國際 BGP 齊全 | 最便宜，頻寬與流量給得最大方 | 對延遲不敏感的建站、備份、跨境电商後台 |

「香港一定比較快」這句話只對一半。香港贏在延遲與穩定性，輸在價格與流量額度。如果你的網站主要是文字與圖片，東京的性價比往往比香港更合理；如果跑的是即時互動，那多付的錢就值得。

## 維度三：硬體與超售，看不到的那一半

規格表不會寫超售比例，但它決定你實際拿到多少算力。一台 32 核的實體機可以切成 64 個 vCPU，也可以切成 128 個，你拿到的「2 核」在這兩種情況下完全不同。判斷方式有幾個線索：標明 CPU 具體型號與世代（例如 AMD EPYC 9004 系列而不是含糊的「Xeon」）、標明 NVMe SSD 而不是只寫 SSD、以及商家是否公開說明不超售。多數主打大陸優化線路的高價位商家不會明說超售比例，但同價位下給的流量特別大、記憶體特別多，通常就是從超售裡省出來的。

另外三個容易被忽略的規格細節：

- **超量之後怎麼處理。** 停機、限速、另外計費是三種完全不同的結果。限速型（例如超量後降到 4Mbps 但仍可無限使用）適合流量波動大的站，停機型適合流量可預測的業務。
- **頻寬是獨享還是共享。** 標「1Gbps 埠」不等於你能跑滿 1Gbps。
- **續費價。** 首期折扣與循環折扣是兩件事。循環折扣（recurring）代表續費時同樣打折，首期折扣通常只有第一年便宜。

## 用同一套標準看 DMIT

DMIT 是 2017 至 2018 年間成立、主攻大陸優化線路的美系服務商，機房集中在洛杉磯、香港、東京三地，產品分成三條線：

- **Tier 1（T1）**：國際線路，沒有大陸優化，價格最低，超量後限速不斷線。
- **Eyeball（EB）**：以移動 CMIN2／CMI 為主的中階線路，比 Pro 便宜。
- **Premium（Pro）**：三網 CN2 GIA 回程的高階線路，也是大部分評測討論的重點。
- 另外還有 Premium Secure（CN2 GIA 加高防）這類針對攻擊場景的方案。

多個第三方評測都提到 DMIT 不超售、支援支付寶與 PayPal，洛杉磯 Pro／EB 目前也支援自助更換 IP。它的缺點同樣明確：香港 Pro 的價格帶跟一般低價 VPS 完全不在同一個市場，熱門型號經常缺貨。

## DMIT 全方案價格對照

以下價格整理自 2025 至 2026 年多個公開頁面與官網公開資訊。DMIT 在 AN4／AN5 平台切換期間調整過定價，加上東京系列各來源的月付數字略有出入，請把下表當作「篩選用的參考值」，實際金額以下單頁顯示為準。年付價通常為月付乘以十二後的折扣價。

### 洛杉磯 LAX.Pro（三網 CN2 GIA 回程，AMD EPYC 9004）

| 型號 | 規格 | 月流量／頻寬 | 超量後 | 價格 | 選購 |
| --- | --- | --- | --- | --- | --- |
| LAX.Pro.TINY | 1 核／2G／20G SSD | 1TB／1Gbps | 4Mbps 不限量 | $9.99／月，年付 $88.88 | [查看 TINY 方案](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.Pocket | 2 核／2G／40G SSD | 1.5TB／4Gbps | 4Mbps 不限量 | $14.90／月，年付 $159.98 | [查看 Pocket 方案](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.STARTER | 2 核／2G／80G SSD | 3TB／10Gbps | 4Mbps 不限量 | $29.90／月，年付 $322.99 | [查看 STARTER 方案](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.MINI | 4 核／4G／80G SSD | 5TB／10Gbps | 8Mbps 不限量 | $58.88／月，年付 $629.99 | [查看 MINI 方案](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.MICRO | 4 核／4G／160G SSD | 7TB／10Gbps | 8Mbps 不限量 | $74.99／月，年付 $799.99 | [查看 MICRO 方案](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.MEDIUM | 6 核／8G／160G SSD | 15TB／10Gbps | 10Mbps 不限量 | $168.88／月，年付 $1799.99 | [查看 MEDIUM 方案](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.LARGE | 8 核／16G／320G SSD | 25TB／10Gbps | 10Mbps 不限量 | $338.88／月，年付 $3619.99 | [查看 LARGE 方案](https://www.dmit.io/aff.php?aff=12046) |
| LAX.Pro.GIANT | 12 核／24G／640G SSD | 50TB／10Gbps | 10Mbps 不限量 | $619.99／月，年付 $6619.99 | [查看 GIANT 方案](https://www.dmit.io/aff.php?aff=12046) |

洛杉磯 Eyeball（LAX.EB）走三網 CMIN2 回程，入門型號的月付價與 Pro 的 TINY 接近，落在 $9.99／月起，具體型號與庫存變動頻繁。

### 香港 HKG.Pro（CN2 GIA，AMD EPYC 7003）

| 型號 | 規格 | 月流量 | 價格 | 選購 |
| --- | --- | --- | --- | --- |
| HKG.Pro.TINY | 1 核／1G／20G SSD | 500GB／1Gbps | $39.90／月，年付 $478 | [查看 HKG TINY](https://www.dmit.io/aff.php?aff=12046) |
| HKG.Pro.STARTER | 1 核／2G／40G SSD | 1TB／1Gbps | $79.90／月，年付 $958 | [查看 HKG STARTER](https://www.dmit.io/aff.php?aff=12046) |
| HKG.Pro.MINI | 2 核／2G／60G SSD | 1.5TB／1Gbps | $119.90／月，年付 $1438 | [查看 HKG MINI](https://www.dmit.io/aff.php?aff=12046) |
| HKG.Pro.MICRO | 4 核／4G／80G SSD | 2TB／1Gbps | $159.90／月，年付 $1918 | [查看 HKG MICRO](https://www.dmit.io/aff.php?aff=12046) |
| HKG.Pro.MEDIUM | 4 核／8G／160G SSD | 2.5TB／1Gbps | $179.90／月，年付 $2158 | [查看 HKG MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| HKG.Pro.LARGE | 8 核／16G／320G SSD | 3TB／1Gbps | $239.90／月，年付 $2878 | [查看 HKG LARGE](https://www.dmit.io/aff.php?aff=12046) |
| HKG.Pro.GIANT | 8 核／24G／640G SSD | 6TB／1Gbps | $499.90／月，年付 $5998 | [查看 HKG GIANT](https://www.dmit.io/aff.php?aff=12046) |

### 香港 HKG.EB（三網 CMIN2／CMI 回程）

| 型號 | 規格 | 月流量／頻寬 | 價格 | 選購 |
| --- | --- | --- | --- | --- |
| HKG.EB.TINY | 1 核／1G／20G SSD | 1TB／1Gbps | $29.90／月，年付 $358 | [查看 HKG EB TINY](https://www.dmit.io/aff.php?aff=12046) |
| HKG.EB.STARTER | 1 核／2G／40G SSD | 2TB／2Gbps | $59.90／月，年付 $718 | [查看 HKG EB STARTER](https://www.dmit.io/aff.php?aff=12046) |
| HKG.EB.MINI | 2 核／2G／60G SSD | 3TB／2Gbps | $89.90／月，年付 $1078 | [查看 HKG EB MINI](https://www.dmit.io/aff.php?aff=12046) |
| HKG.EB.MICRO | 4 核／4G／80G SSD | 4TB／4Gbps | $129.90／月，年付 $1558 | [查看 HKG EB MICRO](https://www.dmit.io/aff.php?aff=12046) |
| HKG.EB.MEDIUM | 4 核／8G／160G SSD | 6TB／4Gbps | $199.90／月，年付 $2398 | [查看 HKG EB MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| HKG.EB.LARGE | 8 核／16G／320G SSD | 12TB／4Gbps | $389.90／月，年付 $4678 | [查看 HKG EB LARGE](https://www.dmit.io/aff.php?aff=12046) |

### 東京 TYO.Pro（CN2 GIA，入門價最低的高階線路）

| 型號 | 規格 | 月流量 | 參考價格 | 選購 |
| --- | --- | --- | --- | --- |
| TYO.Pro.TINY | 1 核／1G／20G SSD | 500GB／1Gbps | $21.90／月，年付約 $262 | [查看 TYO TINY](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.STARTER | 1 核／2G／40G SSD | 1TB／1Gbps | 約 $39.90／月，年付約 $478 | [查看 TYO STARTER](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.MINI | 2 核／2G／60G SSD | 2TB／1Gbps | 約 $79.90／月，年付約 $958 | [查看 TYO MINI](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.MICRO | 2 核／4G／80G SSD | 4TB／1Gbps | 約 $159.90／月，年付約 $1918 | [查看 TYO MICRO](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.MEDIUM | 4 核／8G／160G SSD | 5TB／1Gbps | 約 $259.90／月，年付約 $3118 | [查看 TYO MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.LARGE | 8 核／16G／320G SSD | 8TB／1Gbps | 約 $429.90／月，年付約 $5158 | [查看 TYO LARGE](https://www.dmit.io/aff.php?aff=12046) |
| TYO.Pro.GIANT | 8 核／24G／640G SSD | 15TB／1Gbps | 約 $799.90／月，年付約 $9598 | [查看 TYO GIANT](https://www.dmit.io/aff.php?aff=12046) |

東京 Pro 的超量處理是停機而非限速，這點在挑流量方案時要一起算進去。

### Tier 1 國際線路系列（洛杉磯／香港／東京）

| 型號 | 規格（以洛杉磯為例） | 月流量／頻寬 | 超量後 | 價格 | 選購 |
| --- | --- | --- | --- | --- | --- |
| T1.WEE | 1 核／1G／20G SSD | 1TB／4Gbps | 洛杉磯 100Mbps、港日 50Mbps 不限量 | $36.90／年 | [查看 T1.WEE](https://www.dmit.io/aff.php?aff=12046) |
| T1.TINY | 1 核／2G／40G SSD（香港為 1 核 1G／20G） | 2TB／4Gbps | 100–200Mbps 不限量 | $6.90／月，$76.90／年 | [查看 T1.TINY](https://www.dmit.io/aff.php?aff=12046) |
| T1.STARTER | 2 核／2G／40G SSD | 4TB／10Gbps | 100–200Mbps 不限量 | $12.90／月，$154.80／年 | [查看 T1.STARTER](https://www.dmit.io/aff.php?aff=12046) |
| T1.MINI | 2 核／4G／80G SSD | 8TB／10Gbps | 100–200Mbps 不限量 | $21.90／月，$262.80／年 | [查看 T1.MINI](https://www.dmit.io/aff.php?aff=12046) |
| T1.MICRO | 4 核／4G／80G SSD | 16TB／10Gbps | 200–500Mbps 不限量 | $32.90／月起 | [查看 T1.MICRO](https://www.dmit.io/aff.php?aff=12046) |
| T1.MEDIUM | 4 核／8G／160G SSD | 32TB／10Gbps | 200–500Mbps 不限量 | $49.90／月起 | [查看 T1.MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| T1.LARGE | 8 核／16G／320G SSD | 64TB／10Gbps | 500Mbps 不限量 | $99.90／月起 | [查看 T1.LARGE](https://www.dmit.io/aff.php?aff=12046) |
| T1.GIANT | 8 核／24G／640G SSD | 128TB／10Gbps | 1Gbps 不限量 | $199.90／月起 | [查看 T1.GIANT](https://www.dmit.io/aff.php?aff=12046) |

T1 的定位很清楚：給不需要大陸優化的人用。它的單位流量價格是整個產品線裡最低的，拿來跑備份、圖片站、CDN 源站很划算；如果你的訪客全在大陸，買 T1 大概會失望。

### 過去常見的限量與補貨款

DMIT 會不定期放出限定型號（例如洛杉磯的 MALIBU、CORONA，香港的 Victoria，東京的 Shinagawa），價格通常比常規型號低一截，但庫存不穩定。以下是幾個曾在 2025 年補貨記錄中多次出現的型號，價格為當時的活動價：

| 型號 | 規格 | 活動價 | 選購 |
| --- | --- | --- | --- |
| HKG.Pro.Victoria | 1 核／2G／60G／500Mbps | $298.88／年 | [查看 Victoria 方案](https://www.dmit.io/aff.php?aff=12046&pid=178) |
| TYO.Pro.Shinagawa | 1 核／2G／60G／500Mbps | 約 $199–239.9／年 | [查看 Shinagawa 方案](https://www.dmit.io/aff.php?aff=12046&pid=179) |
| LAX.Pro.PalmSpring | 2 核／2G／40G／2Gbps | $100／年 | [查看 PalmSpring 方案](https://www.dmit.io/aff.php?aff=12046&pid=182) |

這類型號買到就算賺到，沒貨也不用等，直接看常規系列就好。

## 目前的折扣與使用條件

DMIT 的折扣分兩種：官方常態折扣與限時優惠碼。

**官方常態折扣（不需優惠碼）**：洛杉磯 Pro 的 TINY 型號年付約 75 折，其餘型號年付約 9 折。這是結帳時自動帶入的。

**限時優惠碼**（實際可用性與適用範圍會變動，下單前請在結帳頁測試）：

- `2025-XMAS-LAX-PRO-EB-ANNUALLY-STARTER-AND-HIGHER-15OFF-RECURRING`：洛杉磯 Pro／EB 年付 STARTER 及以上，15% 折扣加 10% 返現，屬循環折扣。
- `2025-XMAS-LAX-PRO-EB-10-OFF-RECURRING`：洛杉磯 Pro／EB 常規型號，10% 折扣加 5% 返現。
- `202510_HKG_TYO_PRO_20OFF_RECURRING`：香港 Pro／東京 Pro 季付及以上 8 折，循環折扣。
- 香港與東京的 T1 系列另有多組季付／年付 7 折、月付 9 折的專用碼，型號不同碼也不同。

看到這裡有個重點：帶 `RECURRING` 的碼續費同樣打折，這比首期 5 折實際得多。挑方案時把「續費價」算進去，兩年總支出常常跟第一年的印象完全相反。

## 依情境排的推薦順序

- **訪客主要在大陸、對速度敏感**：香港 Pro 優先。預算繃不住就退到東京 Pro，延遲多 30ms 上下，價格便宜一大截。
- **想用最低成本試 CN2 GIA**：洛杉磯 Pro.TINY，年付不到 90 美元，是這個產品線裡最容易被拿來當「入門體驗」的型號。
- **移動用戶為主**：Eyeball 系列（CMIN2／CMI 回程）比 Pro 更對症，價格也低一級。
- **只要國際線路、跑大流量**：T1 系列，超量限速不斷線，適合圖片站與備份。
- **常被打的業務**：往 Premium Secure 這類高防方案看，一般線路的高防能力不該當成預設值。

## 下單前的檢查清單

1. 先拿測試 IP 在晚高峰實測，別只看商品頁的形容詞。
2. 確認超量後的處理方式是限速還是停機，尤其東京 Pro 屬於停機。
3. 看清楚折扣是首期還是循環。
4. 熱門型號缺貨是常態，缺貨時先想好替代型號，不要臨時改買規格不合的。
5. 付款前確認官網當下的退款與服務條款，各家條款改動頻率高。

**VPS 比較最後還是回到那三題**：訪客在哪、對延遲多敏感、月流量要多少。硬體規格擺在最後看，因為在優化線路這個市場裡，線路與機房早就決定了八成體驗。如果你的答案落在「大陸訪客 + 需要穩定」，那 DMIT 的三條產品線已經涵蓋了從 $6.9／月到數百美元／月的完整區間，剩下要做的只是挑對那一格。
