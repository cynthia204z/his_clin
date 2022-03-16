## 問題紀錄

### Table: chred_sheet_def

1. 不清楚 `SHEET_STYLETYPE` 的功能
2. `SHEET_TYPE` 只有中文，沒有代碼對應
3. `DOCUMENT_CODE` 只存了中文，並且沒有被用來串任何資料

### Freelancer(UEditor)

> 經與世昌大哥討論後，需要請Freelancer處理的部分

1. 只讀模式中，部分控件沒有被禁止：input沒有被禁止，checkbox時好時壞，其他缺乏測試

   操作影片：https://share.vidyard.com/watch/LJVCpFKKhyyA86PQD4CfiD?

2. 新建的病歷抓不到部分控件的html/純文字，但 chred_trans_dtl 中有存到

3. 儲存 chred_trans_dtl 時有 Bug

   EX：無勾選的 checkbox 控件經儲存後，`ITEM_VALUE` 會被填入別人的值

   操作影片：https://share.vidyard.com/watch/27QotYu1uS6ZdBWAMHGCLY?

4. 儲存後重新查詢，資料不完整 (控件中只有 input 讀得出資料，其他種類控件無法 )

   EX： checkbox 無論有沒有值，UI上全部都會變成無勾選狀態

   操作影片：https://share.vidyard.com/watch/jCL79LGb6eGX9fmhmw1uYL?

5. 希望針對`editor.execCommand()`做說明，有哪些參數是可以利用的

6. 因應可能會從外部帶資料進文本編輯區 (EX：病患性別、姓名等)，需要除了<u>在游標位置輸入</u>以外的控件賦值方法


### 版本控制

1. 請世昌大哥開病歷組件的gitlab project

### 已做的修改

#### 【前端】

src/APP.vue

1. props參數

   - mod(審閱模式)：`edit`/`readonly`/`review`/`trace`

     >1. 只能從外部代入，控件上修改模式無效（但尚未依照模式隱藏UI）
     >2. review(審閱) / trace(留痕) 未做

   - searchKind(查詢模式): `DEFAULT`/`SHEET_TYPE`/`TRANS_ID`

   - query(查詢條件)：transId, encounterNo, chartNo, sheetId, sheetType

   ```js
   	props: {
       mod: {
         type: String,
         default: "edit" // edit / readonly / review / trace
       },
       searchKind: {
         type: String,
         default: 'DEFAULT'  // TRANS_ID / DEFAULT / SHEET_TYPE
       },
       query: {
         type: Object,
         default() {
           return {
             transId: undefined, // EX: f47ac190-16da-11ec-930f-cd727fb1098a
             encounterNo: undefined, // EX: I2021071201
             chartNo: undefined, // EX: 1050888
             sheetId: undefined, // EX: N008
             sheetType: undefined, // EX: 檢查記錄單
           }
         }
       }
     },
   ```

   

2. UI：

   - 左側樹型選單顯示與否 (模式二 (`searchKind === 'TRANS_ID'`)不顯示)
   - 加樹型選單項目icon

3. 功能：

   - 新建病歷表單 (利用樹型下拉框選擇病歷模板)，查詢條件要代入 encounterNo & chartNo

     ```js
     handleNewTransMst(sheetId){
     	// 由下拉框的change事件觸發，取得當前選則的病歷模板
     },
     
     addTransMst(){
       // 將選擇的病歷模板設置到文本編輯區
       // 此步驟尚未更動資料庫，編輯完按下儲存鈕後才會更新到資料庫並更新左側樹型選單  
     },
     ```

   - 模式一

     1. 源碼：樹型的葉子 (最後一層選項) 中的資料是病歷模板 (chred_sheet_def)，點選葉子取得特定病歷模板 (`SHEET_ID`) 後，查詢交易主檔中使用該模板的第一筆資料 (不能附加其他條件) 

        => 沒有辦法取得特定病患的病歷、顯示多張同類表單

        ```js
        // 1. 取得所有病歷模板
        getList(){},
          
        // 2. 取得所有模板分類資料夾
        getOrderTree(){},
          
        // 3. 遞迴判斷模板與資料夾的關係，將模板塞到正確的資料夾底下
        getChildren(){},
          
        // 4. 點擊樹型選項，取得病歷模板的SHEET_ID，並用SHEET_ID查詢交易主檔
        conceptTreeNodeClick(data){
          let html = data.SHEET_HTML
          transmstInfo({SHEET_ID:data.SHEET_ID}).then(res => {
            // ※問題：一個SHEET_ID可以對應很多個交易主檔項目，不能保證查出來只有一筆
            // 這裡應該原本是將第一筆資料的html設置給文本編輯區，但不清楚為何註解掉並設置成模板的html
            this.editor.setContent(html)
            // this.editor.setContent(transList[0].SHEET_HTML)
          }).catch(() => {
            // 無法取得交易主檔的話，就將模板的html設置給文本編輯區
            this.editor.setContent(html)
          })
        }
        ```

     2. 修改：樹型選單僅顯示依照查詢條件取得的病歷 

        => 讓葉子變成交易主檔 (chred_trans_mst)，同病歷表單可以顯示多張，並且載入組件時可利用其他條件做查詢 (encounterNo、chartNo、sheetType)

        ```js
        /* searchKind === 'DEFAULT' */
        
        // 1. 取得所有病歷模板
        getList(){},
          
        // 2. 取得所有模板分類資料夾
        getOrderTree(){
          // 新增程式碼：複製樹型，給新增病歷時選擇模板用的下拉框
        },
          
        // 3. 依照外部帶進來的條件，查詢交易主檔
        getTransMst(){
          transmstInfo(query).then(res => {
            // 4. 事先對應模板和交易主檔的關係，設置樹型選項的文字及FORDER_ID(資料夾分類)
            // 5. 將帶有FORDER_ID的交易主檔項目塞到對應的資料夾底下
            this.orderTreeData.forEach(folder => {
              this.getChildren(folder)
            })
          })
        },
          
        // 4. 點擊樹型選項，用傳入的TRANS_ID查詢交易主檔
        conceptTreeNodeClick(data){
          let html = data.SHEET_HTML
          transmstInfo({TRANS_ID: data.TRANS_ID}).then(res => {
            // ※解決：一個TRANS_ID只對應一個交易主檔項目，可以保證查出來只有一筆
            // 將查詢到的資料html設置給文本編輯區
            let trans = response.data.result.rows[0]
            this.editor.setContent(trans.SHEET_HTML)
          }).catch(() => {
            // 無法取得交易主檔的話，就將模板的html設置給文本編輯區
            this.editor.setContent(html)
          })
        }
        ```

        ```js
        /* searchKind === 'SHEET_TYPE' */
        
        // 1. 用sheetType查詢交易主檔
        getTransMstBySheetType(){
          getTransmstBySheetType(query).then(res => {})
        },
        ```

     3. 備註：由於查詢 `encounterNo/chartNo/sheetId/transId` 的 API 和 查詢 `sheetType` 的 API 不同、樹型資料不同，所以模式一有兩種 `searchKind`，前者為 `DEFAULT`，後者為 `SHEET_TYPE`，引用組件時需要依照查詢條件的不同使用不同的 `searchKind`

        ```js
        created() {
          if (this.searchKind === 'DEFAULT') {
            this.getList()
          } else if (this.searchKind === 'SHEET_TYPE') {
            this.getTransMstBySheetType()
          } else if (this.searchKind === 'TRANS_ID') {
            this.getFormByTransId()
          }
        }
        ```

   - 模式二

     1. 只依照 TRANS_ID 查出一張表單，設置到文本編輯區並隱藏樹型選單。

        ```js
        /* searchKind === 'TRANS_ID */
        getFormByTransId(){
          transmstInfo(query).then(res => {})
        }
        ```



src/api/transmst.js

新增用 sheetType 查詢交易主檔的API

```js
// get transmstInfo by sheetType
export function getTransmstBySheetType(query){
  return request({
    url: '/api/transmst/transmstInfo/getTransmstBySheetType',
    method: 'get',
    params: query
  })
}
```



#### 【後端】

app/routes/transmst.routes.js

新增路由

```js
router.get("/transmstInfo/getTransmstBySheetType", transmsts.getTransmstBySheetType);
```

app/controllers/transmst.controller.js

新增查詢方法

```js
exports.getTransmstBySheetType = (req, res) => {}
```



#### 備註

查詢需求：

API: `/api/transmst/transmstInfo`

Table: chred_trans_mst

- [x] SHEET_ID (原有)
- [x] TRANS_ID (新增)
- [x] CHART_NO (新增)
- [x] ENCOUNTER_NO (新增)
- [x] SHEET_ID + CHART_NO (新增)
- [x] SHEET_ID + ENCOUNTER_NO (新增)

API: `/api/transmst/transmstInfo/getTransmstBySheetType`  (新增)

Table: chred_sheet_def + chred_trans_mst

- [x] SHEET_TYPE (chred_sheet_def)
- [x] SHEET_TYPE (chred_sheet_def) + ENCOUNTER_NO (chred_trans_mst)
- [x] SHEET_TYPE (chred_sheet_def)  + CHART_NO (chred_trans_mst)

API: `/api/transdtl/transdtlinfo/:sheet_id`  => `/api/transdtl/transdtlinfo/:trans_id ` (修改)

Table: chred_trans_dtl

- [ ] SHEET_ID (刪除)
- [x] TRANS_ID (新增)