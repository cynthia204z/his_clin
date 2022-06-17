# DEMO 第二階段 NIS 需求修改清單

> 【btn】按鈕需中文
>
> 【patInfo】自動帶入病患資料
>
> 【readonly】只讀輸入框改文字，避免使用者以為可以編輯

## step 1

- [x] ①護理病患清單：預設查詢出清單
- [ ] ①護囑主頁-病患資訊卡：診斷來源 <span style="color: skyblue">=> 不是資料庫有的欄位，需後端幫助</span>
- [x] ①護囑主頁-病患資訊卡：調整排版(生日/年齡)
- [x] ①護囑主頁：隱藏動向(menu)
- [x] ①改醫囑確認藥囑確認menu名(new/測試等等移除)
- [ ] ①醫囑確認 nis3023：Panel01 真實新增耗材 <span style="color: orange">(完成新增彈窗真實資料帶回，尚未儲存)</span>
- [ ] ①醫囑確認 nis3023：Panel02 真實耗材連帶項 <span style="color: skyblue">=> UI完成等後端</span>
  - [x] UI
  - [ ] CRUD
- [x] ①醫囑確認 nis3023：Panel02 新增按鈕二擇一
- [x] ①醫囑確認 nis3023：【btn】
- [x] ①醫囑確認 nis3023：執行清單加勾選欄位 <span style="color: orange">(UI加了，但沒有和欄位值連動)</span>
- [ ] ①藥囑確認 nis3031：真實新增耗材 
- [ ] ①藥囑確認 nis3031：真實耗材連帶項 <span style="color: skyblue">=> UI完成等後端</span>
  - [x] UI
  - [ ] CRUD
- [x] ①藥囑確認 nis3031：【btn】
- [ ] ①藥囑確認 nis3031：藥品屬性圖示 <span style="color:red">=> 確定部分是用CSS組出來的</span> <span style="color: skyblue">=> 需要用 medCode 串 comMedAttribute 的attributeKind => 等後端</span>
- [ ] ①藥囑確認 nis3031：藥品提示 <span style="color:violet">(↑等藥品圖示)</span>
- [x] ①藥囑確認 nis3031：執行清單加勾選欄位 <span style="color: orange">(UI加了，但沒有和欄位值連動)</span>
- [x] ①退藥作業 nis3040：移除無用按鈕，有功能的加tooltip
- [x] ①退藥作業 nis3040：【btn】
- [x] ①照會回覆 nis7020S：【patInfo】
- [ ] ①照會回覆 nis7020S：<kbd>回覆</kbd><span style="color: yellow">【照會單編輯】照會種類疑似會帶出動態表單 </span>
- [ ] ①照會作業 nis7020：【patInfo】
- [ ] ①照會作業 nis7020：真實新增 <span style="color: skyblue">=> 需確認需不需要後端幫助</span>
- [ ] ①交班作業 nis8030：醫囑藥囑資料串接 <span style="color: skyblue">=> 需確認需不需要後端幫助</span>
- [x] ①交班 nis8020：【patInfo】
- [x] ①交班 nis8020：【btn】
- [ ] 交班nis8020改成**交辦事項**，移到交班作業nis8030的其中一個標籤頁(有新增一個list)

## step 2

- [ ] ②醫囑清單 nis3070：真實查出資料 <span style="color: skyblue">=> 需確認需不需要後端幫助</span>
- [ ] ②耗材使用查詢 nis3080：真實查出資料 <span style="color: skyblue">=> 需確認需不需要後端幫助</span>
- [ ] ②看護申請 nis3090：真實新增 <span style="color: orange">=> 班別預設值帶日班</span>
- [ ] ②看護申請 nis3090：form【patInfo】
- [ ] ②看護申請 nis3090：static demo data
- [ ] ②緊急醫令 nis3111：【btn】
- [ ] ②衛教作業 nisB020：debug-新增後無法填打評值

## step 3

- [ ] ③交班 nis8020：病人清單/病患資訊/TPR
- [ ] ③出院護理 nis9020：掛OBS
- [ ] ③計畫 nis5020：OBS應用模式三
- [ ] ③護理紀錄：OBS應用模式三

## 其他

- [ ] <span style="color: gray">醫囑確認 nis3023：加雙擊進入searchList</span>
- [ ] <span style="color: gray">藥囑確認 nis3031：加雙擊進入searchList</span>
- [x] <span style="color: gray">照會回覆 nis7020S：【readonly】</span>
- [ ] <span style="color: gray">照會作業 nis7020：【readonly】</span>
- [ ] <span style="color:gray">交班作業：把patInfo提出來用</span>