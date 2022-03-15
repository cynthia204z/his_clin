### HIS7住院護囑前端報錯

**錯誤訊息**：

<span style="background:#692424;color:#FFB3B3;padding:3px;border-radius:3px;font-family:Courier;font-size:14px"> The data property "list" is already declared as a prop. Use prop default value instead.</span>

**原因**：企業組件mixin中已宣告list，不能再prop同名變數

**問題**：在父組件裡面查完資料給list賦值後用prop傳給子組件，但子組件(ListBox)的企業組件mixin中存在已宣告的list，所以不能在props中重複宣告

**解決方法**：

1. refs到子組件裡面再做request  <span style="color:#89A39C">➡因為住院護囑用這個改起來比較方便所以下列清單都用此方式</span>
2. 用其他變數名稱，在子組件watch變化賦值給子組件中的list



> **※備註 1**
>
> 由於企業組件不能更動所以選擇避開prop的方式。
>
> 如果是一般情況，可以去掉子組件data裡面定義的list，並使用props的default值代替（錯誤訊息中建議的做法）。
>
> 
>
> **※備註 2**
>
> 如果是一般情況，可以用mixins/pageCommon/list中dataForm的作法(computed + props)。
>
> 但不適用於企業組件中已經存在data裡的list，computed再定義一次的話會報另一個錯誤訊息：
>
> <span style="background:#692424;color:#FFB3B3;padding:3px;border-radius:3px;font-family:Courier;font-size:13px">The computed property "list" is already defined in data.</span>





已修改並測試：

- [x] 【nis3031 藥囑確認Test(新版)】
  - [x] 醫囑藥囑作業
  - [x] 耗材連帶項
- [x] 【nis3023 醫囑確認New】
  - [x] 醫囑處置作業
  - [x] 文字醫囑
- [x] 【nis3070 醫囑清單】
  - [x] 醫囑
  - [x] 藥囑
- [x] 【nis6030 化療確認】
  - [x] 化療總表
  - [x] 化療藥囑確認
    - [x] 化療藥囑確認
    - [x] 耗材連帶項
  - [x] 化療照護紀錄表
  - [x] 化療資訊
- [x] 【nis3111 緊急醫令】
  - [x] leftTable
  - [x] rightTable
  - [x] addForm
- [x] 【nis3040 退藥作業】
- [x] 【nis3080 耗材使用查詢】
- [x] 【nis3110 帳務查詢】
- [x] 【nis7020 照會作業】
  - [x] 照會
  - [x] 會診
- [x] 【nis7020S 照會回覆】
- [x] 【nis8020 交班】
  - [x] leftTable
  - [x] rightTable
- [x] 【nis8030 交班作業】
  - [x] 醫囑
  - [x] 藥囑
  - [x] 會診
  - [x] 手術
  - [x] 飲食
  - [x] 輸血
  - [x] 健康問題
- [x] 【nis8040Table 跨單位交班查詢】
- [x] 【nis8050 簽收】
- [x] 【nis9020 出院護理】
  - [x] 護理指導總表
  - [x] 護理計畫總表
  - [x] 護理照會及會診總表
- [x] 【nisB020 衛教作業】





其他報錯

【nis9020 出院護理】

- [x] 出院摘要與護理：el-checkbox-group v-model綁定值為undefined