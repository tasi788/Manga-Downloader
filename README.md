#  最新漫畫下載器

## 使用程式語言
- Python3

### 套件需求
- requests
- bs4
- re
- collections
- os
- time
- base64
- pyaes

## 漫畫來源
 [漫畫堆](https://www.manhuadui.com/) (https://www.manhuadui.com/)
 
## 特色
- 能夠自動擷取喜愛的漫畫 最新更新時間、最新漫畫名稱
- 能夠依據最新更新時間做排列顯示
- 能夠選取漫畫不同類別 (e.g.本傳、番外篇等)
- 支援下載最新集數、或是一次全部下載
- 下載時會自動建立漫畫名稱、漫畫集數名稱的資料夾
- 所有套件皆支援在 **iOS手機平台** 上的 [Pyto](https://apps.apple.com/tw/app/pyto-python-3-7/id1436650069) 應用程式內安裝並執行

## 使用教學
變數 **web** 為喜愛的漫畫清單。變數 **web** 為 **dict** 型態。請依照`”中文名稱”: “在漫畫堆中的網址代號”, `格式插入變數 **web** 的**括號**內。
    
- 範例: `“鬼滅之刃”: “guimiezhiren”, `

## 執行結果範例

```no-highlight
正在統整最新漫畫更新時間...

現在時間 2019-10-26 15:37
-----------
1: 鬼滅之刃  最新更新時間: 2019-10-25 19:05
    章節  最新集數: 180话 恢复
-----------
2: 擅長捉弄人的高木同學  最新更新時間: 2019-10-24 05:19
    章節  最新集數: 113话
-----------
3: 錢進球場  最新更新時間: 2019-10-23 00:51
    章節  最新集數: 144话
-----------
4: 擅長捉弄人的原高木同學  最新更新時間: 2019-10-23 00:18
    章節  最新集數: 109话
-----------
5: 一拳超人  最新更新時間: 2019-10-18 04:01
    章節  最新集數: 161话
    原作版  最新集數: 原作版117话
    番外  最新集數: 16话番外
-----------
6: 進擊的巨人  最新更新時間: 2019-10-09 12:02
    章節  最新集數: 122话东立版

請輸入下載漫畫的編號: 4
要下載哪一回?
 註: 下載最新集數請輸入 "latest"; 下載全部請輸入 "all"
latest
即將下載漫畫名稱: 109话
網址: http://www.manhuadui.com/manhua/shanchangzhuonongrendeyuangaomutongxue/418543.html
共 9 頁
第 8 頁下載完成
已完成下載 109话

是否繼續下載 (y/n): n
已結束程式...
```
註: 有些編譯器不支援處理 **print** 函數內的 `\r` (游標回到行首) 字元，所以在下載個別分頁時會依序顯示 `第 X 頁下載完成` ，而非只顯示一行。

## 漫畫下載原理
進入**漫畫堆**網頁的漫畫頁面時，並非一開時就載入好漫畫圖片的位置。**漫畫堆**使用 JavaScript 動態生成圖片顯示的 HTML code。所以無法直接使用 **request** 套件下載圖片。

該網頁會事先傳送各分頁的圖片連結，並透過**AES CBC**方式加密。解密的 **金鑰** 與 **IV(初始向量)** 皆可透過爬蟲解析擷取下來。接著使用**純Python**套件的 **pyaes** (**iOS平台** 上的 **Pyto** 程式支援安裝此套件) 或是一般較常用的 **PyCrypto** 套件做AES解密。

後續只要再做些文字處理即可取得各分頁的圖片連結，並透過 **requests** 套件下載。

---

## 警語⚠️
本程式僅供作為**Python程式語言應用範例**之教學用途，請勿使用於任何非法行為
