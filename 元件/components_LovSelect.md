# 1. LovSelect 分頁/滾動式查詢下拉

![image-20210706094052285](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210706094052285.png)

![image-20210706094136459](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210706094136459.png)

- 使用方式：直接使用`<LovSelect></LovSelect>`標籤

  屬性：

  - **type**：用`type="page"`(分頁) 或`type="scroll"`(滾動加載) 指定下拉類型，<font style="color:red">沒有預設值，一定要傳</font>
  - **apiUrl**：從哪支api GET資料，類型String
  - **lovQueryColume**：去後端當查詢參數的欄位(輸入框打的是哪個欄位的內容)，類型Object
  - **lovColumeList**：選項文字設定，類型Array
  - **optionLabel**：選項顯示的文字根據哪個欄位，類型String
  - **optionValue**：選項實際上的值根據哪個欄位，類型String
  - **lovEvent**：接收選擇的資料
  - **selectChange**：記錄當前行
  - **parent-value.sync**：雙向綁定父組件狀態

  ```html
  <el-table-column label="病歷號碼" algin="left">
    <template slot-scope="scope">
      <LovSelect
                 :parent-value.sync="scope.row.chartNo"
                 type="page"
                 :apiUrl="selectApi"
                 :lovQueryColume="lovQueryColume"
                 :lovColumeList="lovColumeList"
                 optionLabel="chartNo"
                 optionValue="chartNo"
                 @lovEvent="lovEvent"
                 @selectChange="selectChange(scope.row)"
                 ref="lovSelect"
                 ></LovSelect>
    </template>
  </el-table-column>
  ```
  
  ```js
  export default{
    data() {
      return {
        selectApi: "/api/his7/com/chartinfo/ComChrbas", // api url
        lovQueryColume: { // 去後端當查詢參數的欄位(輸入框打哪個欄位的內容)
          // 欄位名稱：符合類型的預設值
          chartNo: undefined,
        },
        lovColumeList: [ // 選項設定
          {
            label: "", // 選項標題
            content: "chartNo", // 欄位名稱
          },
          {
            label: "",
            content: "patName",
          },
          {
            label: "",
            content: "birthDate",
          },
          {
            label: "",
            content: "idNo",
          },
        ],
        selectItemData: {}, // 儲存子組件傳過來的資料
        currentRow: {}, // 儲存table當前行資料
        selectItemDataState: false, //是否接收到子組件傳來的資料
      }
    },
    watch: {
      // 監聽從子組件接受到資料的狀態變化
      selectItemDataState: {
        handler(val) {
          if (!val && val != false) return;
          this.changeColumeValue();
        },
        deep: true,
      },
    },
    methods: {
      // 接收從子組件(lovselect)傳來的資料
      lovEvent(data) {
        if (data) {
          this.selectItemData = data;
          // 表示收到資料
          this.selectItemDataState = true;
        }
      },
      // 記錄table當前行
      selectChange(row) {
        this.handleChange(row);
        this.currentRow = row;
      },
      // 收到資料後，給table對應欄位塞值
      changeColumeValue() {
        for (let i = 0; i < this.list.length; i++) {
          if (this.currentRow.id === this.list[i].id) {
            // ---請依table需求更改欄位名稱---
            this.list[i].inNo = this.selectItemData.idNo;
            this.list[i].patName = this.selectItemData.patName;
            this.list[i].birthDate = this.selectItemData.birthDate;
          }
        }
        this.selectItemDataState = false;
      },
    }
  }
  ```
  
  

## 1.1 Edit Page

  ```html
  <el-table-column prop="chartNo" label="病歷號碼" algin="left">
    <template slot-scope="scope">
      <LovSelect
                 :parent-value.sync="scope.row.chartNo"
                 type="page"
                 :apiUrl="selectApi"
                 :lovQueryColume="lovQueryColume"
                 :lovColumeList="lovColumeList"
                 optionLabel="chartNo"
                 optionValue="chartNo"
                 @lovEvent="lovEvent"
                 @selectChange="selectChange(scope.row)"
                 ref="lovSelect"
                 ></LovSelect>
    </template>
  </el-table-column>
  ```


  ```js
  export default{
    data() {
      return {
        selectApi: "/api/his7/com/chartinfo/ComChrbas",
        lovQueryColume: {
          chartNo: undefined,
        },
        lovColumeList: [
          {
            label: "",
            content: "chartNo",
          },
          {
            label: "",
            content: "patName",
          },
          {
            label: "",
            content: "birthDate",
          },
          {
            label: "",
            content: "idNo",
          },
        ],
        selectItemData: {},
        currentRow: {},
        selectItemDataState: false,
      }
    },
    watch: { 
      selectItemDataState: {
        handler(val) {
          if (!val && val != false) return;
          this.changeColumeValue();
        },
        deep: true,
      },
    },
    methods: {
      lovEvent(data) {
        if (data) {
          this.selectItemData = data;
          this.selectItemDataState = true;
        }
      },
      selectChange(row) {
        this.handleChange(row);
        this.currentRow = row;
      },
      changeColumeValue() {
        for (let i = 0; i < this.list.length; i++) {
          if (this.currentRow.id === this.list[i].id) {
            this.list[i].inNo = this.selectItemData.idNo;
            this.list[i].patName = this.selectItemData.patName;
            this.list[i].birthDate = this.selectItemData.birthDate;
          }
        }
        this.selectItemDataState = false;
      },
    }
  }
  ```



## 1.2 Search 

  ```html
  <el-form-item label="病歷號碼">
    <LovSelect
               :parent-value.sync="query.chartNo"
               type="page"
               :apiUrl="selectApi"
               :lovQueryColume="lovQueryColume"
               :lovColumeList="lovColumeList"
               optionLabel="chartNo"
               optionValue="chartNo"
               ></LovSelect>
  </el-form-item>
  ```





## 1.3 Form

  ```html
  <el-col :span="24">
    <el-form-item label="病歷號碼">
      <LovSelect
                 :parent-value.sync="dataForm.chartNo"
                 type="page"
                 :apiUrl="selectApi"
                 :lovQueryColume="lovQueryColume"
                 :lovColumeList="lovColumeList"
                 optionLabel="chartNo"
                 optionValue="chartNo"
                 @lovEvent="lovEvent"
                 ></LovSelect>
    </el-form-item>
  </el-col>
  ```

  ```js
  lovEvent(data) {
    if (data) {
      this.selectItemData = data;
      this.selectItemDataState = true;
    }
  },
    changeColumeValue() {
      this.dataForm.inNo = this.selectItemData.idNo;
      this.dataForm.patName = this.selectItemData.patName;
      this.dataForm.birthDate = this.selectItemData.birthDate;
      this.selectItemDataState = false;
    },
  ```

  

# 2. 多欄位查詢

- 說明：用戶輸入 關鍵字，從 數據庫中 一次性地 查詢 多個欄位。 

- 比如：要查找 "病患"，在輸入框輸入關鍵字，以該關鍵字從數據庫中以 or 方式模糊查詢多個欄位(包括 病歷號碼、病患姓名、身分證號)。  



## 2.1 前端

![1625810677328](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/1625810677328.gif)

```html
<el-col :span="6">
  <el-form-item label="查詢">
    <LovSelect
               :parent-value.sync="query.keyword"
               type="scroll"
               :apiUrl="selectApi"
               :lovQueryColume="lovQueryColume"
               :lovColumeList="lovColumeList"
               optionLabel="patName"
               optionValue="chartNo"
               placeholder="查詢病歷號碼/姓名/身分證"
               ></LovSelect>
  </el-form-item>
</el-col>
```

```json
selectApi: "/api/his7/com/chartinfo/ComChrbas",
lovQueryColume: {
  keyword: undefined,
},
lovColumeList: [
  {
    label: "",
    content: "chartNo",
  },
  {
    label: "",
    content: "patName",
  },
  {
    label: "",
    content: "birthDate",
  },
  {
    label: "",
    content: "idNo",
  },
],
```



## 2.2 後端

- 在 業務層的實現類 xxxxxServiceImpl 的 `List<ComChrbasEntity> getList(ComChrbasPagination comChrbasPagination)` 方法內 ，加上 "關鍵字查詢" 的代碼 (第8~13行)
  1. 先判斷 ComChrbasPagination 對象內的 屬性 keyword 是否有被賦值
  2. 如果 keyword 有被賦值，則 將所有的查詢目標欄位，以 or 的模糊查詢方式實現

```java
public List<ComChrbasEntity> getList(ComChrbasPagination comChrbasPagination){

  QueryWrapper<ComChrbasEntity> queryWrapper=new QueryWrapper<>();

  //...

  //關鍵字查詢
  if(!"null".equals(String.valueOf(comChrbasPagination.getKeyword()))){
    queryWrapper.lambda()
      .or(t->t.like(ComChrbasEntity::getChartNo,comChrbasPagination.getKeyword())) //目標欄位：病歷號碼
      .or(t->t.like(ComChrbasEntity::getPatName,comChrbasPagination.getKeyword())) //目標欄位：病患姓名
      .or(t->t.like(ComChrbasEntity::getIdNo,comChrbasPagination.getKeyword())); //目標欄位：身分證號
  }

  //...
  
  Page<ComChrbasEntity> page=new Page<>(comChrbasPagination.getCurrentPage(), comChrbasPagination.getPageSize());
  IPage<ComChrbasEntity> userIPage=this.page(page,queryWrapper);
  return comChrbasPagination.setData(userIPage.getRecords(),userIPage.getTotal());
}
```



> 屬性 keyword 的 來源

- JNPF所生成的全部 模型層的 xxxxPagination 類 都會繼承 Pagination

```java
@Data
public class ComChrbasPagination extends Pagination {
```



- 而 Pagination 又會繼承 Page 類

```java
@Data
public class Pagination extends Page{
```



- Page類：
  - 只有一個屬性 keyword，所有每一隻生成出來的程式碼都可以直接以上述方式，實現關鍵字多欄位查詢的功能。

```java
@Data
public class Page {
    @ApiModelProperty(value = "关键字")
    private String keyword="";
}
```

