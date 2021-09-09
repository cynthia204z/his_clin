# 每一支都要加的

```html
<el-button type="primary" icon="el-icon-book" @click="saveRecord()">保存</el-button>

<el-col :span="24">
  <groupTitle content="保險衛材群組" />
</el-col>

<JNPF-table ... @current-change="handleChange"></JNPF-table>
```

```js
selected: [],

  handleChange(val) {
  if (val) {
    this.selected.push(val["id"]);
  }
},
  async saveRecord() {
    let i, j;
    let rec;
    let dataForm = {
      version: 0,
      mtrlGroup: undefined,
      insFeeCode: "",
      creatoruserid: undefined,
      creatortime: undefined,
    };
    for (i = 0; i < this.selected.length; i++) {
      for (j = 0; j < this.list.length; j++) {
        if (this.selected[i] === this.list[j].id) {
          rec = this.list[j];
          await request({
            url: "/api/his7/com/accounting/ComFeeinsmtrlgroupdtl/" + rec.id,
            method: "get",
          }).then((res) => {
            const formatCreatortime = this.$moment(rec.creatortime).format(
              "YYYY-MM-DD HH:mm:ss"
            );
            dataForm = res.data;
            dataForm.version = rec.version;
            dataForm.creatortime = new Date(
              Date.parse(formatCreatortime)
            ).getTime();
            dataForm.creatoruserid = rec.creatoruserid;
            dataForm.insFeeCode = rec.insFeeCode;
            dataForm.mtrlGroup = rec.mtrlGroup;
            request({
              url:
              "/api/his7/com/accounting/ComFeeinsmtrlgroupdtl/" +
              dataForm.id,
              method: "PUT",
              data: dataForm,
            }).then((res) => {
              this.$message({
                message: res.msg,
                type: "success",
                duration: 500,
                onClose: () => {
                  this.visible = false;
                  // this.$emit('refresh', true)
                },
              });
            });
          });
          break;
        }
      }
    }
    this.selected = [];
  },
```



# 樂觀鎖

> index.vue

每個table或form加樂觀鎖欄位

- table

    ```html
    <el-table-column label="版本" prop="version" v-if="show">
      <template slot-scope="scope">
        <el-input v-model="scope.row.version" size="small" controls-position="right" />
      </template>
    </el-table-column>
    ```

- form

    ```html
    <el-col :span="12">
      <el-form-item label="版本" prop="version" v-if="show">
        <el-input v-model="dataForm.version"></el-input>
      </el-form-item>
    </el-col>
    ```

	data

    ```js
    data() {
      return {
        show: false, // 加，隱藏欄位
        // ...
        dataForm: {
          version: 0, // 加樂觀鎖
        },
      };
    },
    ```



隱藏樂觀鎖欄位

```js
show: false
```





# EditPage

## 頁面直接編輯

### 可編輯欄位

#### string

```html
<el-table-column prop="prCondValue" label="催款條件值" align="left">
  <template slot-scope="scope">
    <el-input v-model="scope.row.prCondValue" placeholder="請輸入" size="small" controls-position="right" />
  </template>
</el-table-column>
```



#### number

````html
<el-table-column prop="codelen" label="代碼內容長度"  align="left">
  <template slot-scope="scope">
    <el-input-number v-model="scope.row.codelen" size="small" controls-position="right" />
  </template>
</el-table-column>
````



#### date

改`value-format="yyyy-MM-dd"`

```html
<el-table-column prop="stDate" label="生效日" align="left">
  <template slot-scope="scope">
    <el-date-picker
                    v-model="scope.row.stDate"
                    type="date"
                    placeholder="請選擇"
                    format="yyyy-MM-dd"
                    value-format="yyyy-MM-dd"
                    />
  </template>
</el-table-column>
```



#### time

```html
<el-table-column prop="endTime" label="結束時間" align="left" width="120">
  <template slot-scope="scope">
    <el-time-picker 
                    v-model="scope.row.endTime" 
                    placeholder="請選擇"
                    format="HH:mm"
                    value-format = 'HHmm'
                    >
    </el-time-picker>
  </template>
</el-table-column>
```



#### rediobox

如果{{ }}裡面本來是scope.row.xxx，改成item.fullname

```html
<el-table-column prop="enabled" label="啟用否" algin="left">
  <template slot-scope="scope">
    <el-radio-group v-model="scope.row.enabled" size="medium">
      <el-radio
                v-for="(item, index) in enabledOptions"
                :key="index"
                :label="item.id"
                :disabled="item.disabled"
                >{{ item.fullName | dynamicText(enabledOptions) }}</el-radio>
    </el-radio-group>
  </template>
</el-table-column>
```



#### dropdown(數據接口)

加 `@change="handleChange(scope.row)"`

```html
<el-table-column prop="prCondition" label="催款條件" align="left">
  <template slot-scope="scope">
    <el-select
               v-model="scope.row.prCondition"
               placeholder="請選擇"
               clearable
               :multiple="false"
               @change="handleChange(scope.row)"
               >
      <el-option
                 v-for="(item, index) in prConditionOptions"
                 :key="index"
                 :label="item.F_CODE_DESC"
                 :value="item.F_CODE_NO"
                 :disabled="item.disabled"
                 ></el-option>
    </el-select>
  </template>
</el-table-column>
```

資料來源

```js
export default{
  data(){
    return{
      prConditionOptions: [],
    }
  },
  created() {
    this.getprConditionOptions();
  },
  methods:{
    getprConditionOptions() {
      // 數據街口ID有錯的話可以去數據接口/默認/更多/預覽看
      previewDataInterface("26dd577893694be8ac538d9b6f426eef").then((res) => {
        this.prConditionOptions = res.data;
      });
    },
  }
}
```



### 儲存

```js
async saveRecord() {
  ...
  let dataForm = {
    version: 0,  // 加
    // ...(所有可以直接在頁面上編輯的欄位)
  };
  for (i = 0; i < this.selected.length; i++) {
    for (j = 0; j < this.list.length; j++) {
      if (this.selected[i] === this.list[j].id) {
        ...
        await request({
          ...
        }).then((res) => {
          ...
          // 加
          dataForm.version = rec.version;

          // 如果有日期時間的編輯欄位
          // 轉換時間格式，YYYY-MM-DD HH:mm:ss確保下面轉成timestamp有9位數
          const formatStDate = this.$moment(rec.stDate).format(
            "YYYY-MM-DD HH:mm:ss"
          );
          const formatEdDate = this.$moment(rec.edDate).format(
            "YYYY-MM-DD HH:mm:ss"
          );
          ...
          // 轉換時間格式 → timestamp
          dataForm.stDate = new Date(Date.parse(formatStDate)).getTime()
          dataForm.edDate = new Date(Date.parse(formatEdDate)).getTime()
            ...
            request({
              ...
            }).then((res) => {
              ...
            });
            });
        });
        break;
      }
    }
  }
  this.selected = [];
},
```



鍵盤

# 多表(mst對dtl)

> 整合在dtl資料夾
>
> Form、ExportBox是dtl的元件
>
> Form4Mst、ExportBox4Mst是mst的元件



## 子表popup編輯表單

### 傳入外鍵

> index.vue

看子表的外鍵欄位是什麼，querycodemst裡面就放什麼

```js
querycodemst: {
  prmstId: 0,
},
```

子表popup編輯表單

```js
addOrUpdateHandle(id, isDetail) {
  this.formVisible = true;
  this.$nextTick(() => {
    // 加傳第三個參數（外鍵）
    this.$refs.JNPFForm.init(id, isDetail, this.querycodemst["prmstId"]);
  });
},
```



### 接收外鍵（目前先這樣處理，還沒有統一規範）

> Form.vue

外鍵欄位（禁用）

```html
<!-- 外鍵 -->
<el-col :span="24">
  <el-form-item label="催款類別ID" prop="prmstId">
    <el-input v-model="dataForm.prmstId" disabled :style="{ width: '100%' }"></el-input>
  </el-form-item>
</el-col>
```

![image-20210625111907238](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210625111907238.png)

data

```js
data() {
  return {
    show: false, // 加，隱藏欄位
    // ...
    dataForm: {
      version: 0, // 加樂觀鎖
      // ...
      prmstId: "", // 加外鍵
    },
  };
},
```



```js
// 參數：子表ID，是否唯讀，主表ID
init(id, isDetail, querycodemst) { // 接收第三個參數（主表ID）
  this.dataForm.id = id || 0;
  this.visible = true;
  this.isDetail = isDetail || false;
  console.log(this.dataForm["prmstId"]);
  this.$nextTick(() => {
    this.$refs["elForm"].resetFields();
    // 有子表ID代表是編輯
    if (this.dataForm.id) {
      this.loading = true;
      request({
        url: "/api/his7/com/oweinfo/ComPrDtl/" + this.dataForm.id,
        method: "get",
      }).then((res) => {
        this.dataForm = res.data;
        this.loading = false;
      });
    }else{ // 沒子表ID代表新增：加 else和內容
      // 給dataForm主表ID
      this.dataForm["prmstId"] = querycodemst; 
    }
  });
},
```



## 主表popup編輯表單

### index.vue

表單關閉呼叫index refresh

```js
refresh(isrRefresh) {
  this.formVisible = false;
  this.formVisible4Mst = false; // 加主表表單元件的開啟狀態
  if (isrRefresh) this.reset();
},
```



# 虛擬欄位

## 靜態數據

> 靜態直接用jnpf生成的過濾器用的數據

### EditPage

```html
<el-table-column prop="feeCode" label="計價代碼" algin="left">
  <template slot-scope="scope">
    <el-select
               v-model="scope.row.feeCode"
               placeholder="請選擇"
               clearable
               :style="{ width: '100%' }"
               :multiple="false"
               @change="handleChange(scope.row)"
               >
      <el-option
                 v-for="(item, index) in feeCodeOptions"
                 :key="index"
                 :label="item.id"
                 :value="item.id"
                 :disabled="item.disabled"
                 ></el-option>
    </el-select>
  </template>
</el-table-column>

<el-table-column prop="feeCode" label="計價名稱" algin="left">
  <template slot-scope="scope">
    {{ scope.row.feeCode | dynamicText(feeCodeOptions) }}
  </template>
</el-table-column>
```

### Form

> 主要是 :label 換過濾器用的數據裡面的 id 和 fullName

```html
<el-col :span="24">
  <el-form-item prop="discCode" label="身份代碼" required>
    <el-select
               v-model="dataForm.discCode"
               placeholder="請選擇"
               clearable
               :style="{ width: '100%' }"
               :multiple="false"
               >
      <el-option
                 v-for="(item, index) in discCodeOptions"
                 :key="index"
                 :label="item.id"
                 :value="item.id"
                 :disabled="item.disabled"
                 ></el-option>
    </el-select>
  </el-form-item>
</el-col>

<el-col :span="24">
  <el-form-item prop="discCode" label="身份名稱">
    {{ dataForm.discCode | dynamicText(discCodeOptionsN) }}
  </el-form-item>
</el-col>
```

> 或是計算現有的欄位

```html
<el-col :span="24">
  <el-form-item label="成數" prop="rateNum">
    <el-input-number v-model="dataForm.rateNum" placeholder="數字文本" :step="0.1"></el-input-number>
  </el-form-item>
</el-col>

<el-col :span="24">
  <el-form-item label="成數(%)" prop="rateNum">
    {{(dataForm.rateNum*100).toFixed(1)}}%
  </el-form-item>
</el-col>
```





## 數據接口

### EditPage

```js
data(){
  return{
    chartNoOptions: [], // 數據接口用的
    chartNoOptionsFilter: [] //過濾器用的
  }
}
```

```js
getchartNoOptions() {
  previewDataInterface("e5af74486733420980cc080caa6f1c46").then((res) => {
    this.chartNoOptions = res.data;
    this.$nextTick(() => {
      let i;
      for (i = 0; i < this.chartNoOptions.length; i++) {
        if (this.chartNoOptions[i]) {
          this.chartNoOptionsFilter.push(new Object());
          this.chartNoOptionsFilter[i].id = this.chartNoOptions[i].CHART_NO;
          this.chartNoOptionsFilter[i].fullName = this.chartNoOptions[i].PAT_NAME;
        }
      }
    });
  });
},
```

#### date

```js
getchartNoOptions() {
  previewDataInterface("e5af74486733420980cc080caa6f1c46").then((res) => {
    this.chartNoOptions = res.data;
    this.$nextTick(() => {
      let i;
      for (i = 0; i < this.chartNoOptions.length; i++) {
        if (this.chartNoOptions[i]) {
          this.chartNoOptionsBirthDate.push(new Object());
          this.chartNoOptionsBirthDate[i].id = this.chartNoOptions[i].CHART_NO;
          this.chartNoOptionsBirthDate[i].fullName = this.chartNoOptions[i].BIRTH_DATE;
          this.chartNoOptionsBirthDate[i].fullName = this.$moment(this.chartNoOptionsBirthDate[i].fullName).format("YYYY-MM-DD");
        }
      }
    });
  });
},
```



## Lov



# 關聯/有資料庫欄位的table欄位

## EditPage 

### 數據接口

#### 欄位不可編輯

```html
<el-table-column prop="chartNo" label="病歷號碼" algin="left">
  <template slot-scope="scope">
    <el-select
               v-model="scope.row.chartNo"
               placeholder="請選擇"
               clearable
               :style="{ width: '100%' }"
               :multiple="false"
               @change="selectChange(scope.row)"
               >
      <el-option
                 v-for="(item, index) in chartNoOptions"
                 :key="index"
                 :label="item.CHART_NO"
                 :value="item.CHART_NO"
                 :disabled="item.disabled"
                 ></el-option>
    </el-select>
  </template>
</el-table-column>

<el-table-column prop="patName" label="病患姓名" align="left" />
```

```js
getchartNoOptions() {
  previewDataInterface("e5af74486733420980cc080caa6f1c46").then((res) => {
    this.chartNoOptions = res.data;
    this.$nextTick(() => {
      let i;
      for (i = 0; i < this.chartNoOptions.length; i++) {
        if (this.chartNoOptions[i]) {
          this.chartNoOptionsPatName.push(new Object());
          this.chartNoOptionsPatName[i].id = this.chartNoOptions[i].CHART_NO;
          this.chartNoOptionsPatName[i].fullName = this.chartNoOptions[i].PAT_NAME;
        }
      }
    });
  });
},	
  selectChange(val) {
    this.handleChange(val);
    let i;
    for (i = 0; i < this.list.length; i++) {
      if (this.list[i].id === val.id) {
        for (let j = 0; j < this.chartNoOptionsPatName.length; j++) {
          if (this.list[i].chartNo === this.chartNoOptionsPatName[j].id) {
            this.list[i].patName = this.chartNoOptionsPatName[j].fullName;
          }
        }
      }
    }
  },
```

#### 欄位可編輯

```html
<el-table-column prop="chartNo" label="病歷號碼" algin="left">
  <template slot-scope="scope">
    <el-select
               v-model="scope.row.chartNo"
               placeholder="請選擇"
               clearable
               :style="{ width: '100%' }"
               :multiple="false"
               @change="selectChange(scope.row)"
               >
      <el-option
                 v-for="(item, index) in chartNoOptions"
                 :key="index"
                 :label="item.CHART_NO"
                 :value="item.CHART_NO"
                 :disabled="item.disabled"
                 ></el-option>
    </el-select>
  </template>
</el-table-column>

<el-table-column prop="idNo" label="身分證號" align="left">
  <template slot-scope="scope">
    <el-input
              v-model="scope.row.idNo"
              placeholder
              size="small"
              controls-position="right"
              />
  </template>
</el-table-column>
```

```js
getchartNoOptions() {
  previewDataInterface("e5af74486733420980cc080caa6f1c46").then((res) => {
    this.chartNoOptions = res.data;
    this.$nextTick(() => {
      let i;
      for (i = 0; i < this.chartNoOptions.length; i++) {
        if (this.chartNoOptions[i]) {
          this.chartNoOptionsIdNo.push(new Object());
          this.chartNoOptionsIdNo[i].id = this.chartNoOptions[i].CHART_NO;
          this.chartNoOptionsIdNo[i].fullName = this.chartNoOptions[i].ID_NO;
        }
      }
    });
  });
},
  selectChange(val) {
    this.handleChange(val);
    let i;
    for (i = 0; i < this.list.length; i++) {
      if (this.list[i].id === val.id) {
        for (let j = 0; j < this.chartNoOptionsIdNo.length; j++) {
          if (this.list[i].chartNo === this.chartNoOptionsIdNo[j].id) {
            this.list[i].idNo = this.chartNoOptionsIdNo[j].fullName;
          }
        }
      }
    }
  },
```



## Form

### 數據接口

#### 可編輯

```html
<el-col :span="24">
  <el-form-item label="病歷號碼" prop="chartNo" required>
    <el-select
               v-model="dataForm.chartNo"
               placeholder="請選擇"
               clearable
               :style="{ width: '100%' }"
               :multiple="false"
               @change="selectChange"
               >
      <el-option
                 v-for="(item, index) in chartNoOptions"
                 :key="index"
                 :label="item.CHART_NO"
                 :value="item.CHART_NO"
                 :disabled="item.disabled"
                 ></el-option>
    </el-select>
  </el-form-item>
</el-col>

<el-col :span="24">
  <el-form-item label="病患姓名" prop="patName">
    <el-input
              v-model="dataForm.patName"
              placeholder="請輸入"
              clearable
              :style="{ width: '100%' }"
              ></el-input>
  </el-form-item>
</el-col>
```

```js
getchartNoOptions() {
  previewDataInterface("e5af74486733420980cc080caa6f1c46").then((res) => {
    this.chartNoOptions = res.data;
    this.$nextTick(() => {
      let i;
      for (i = 0; i < this.chartNoOptions.length; i++) {
        if (this.chartNoOptions[i]) {
          this.chartNoOptionsIdNo.push(new Object());
          this.chartNoOptionsIdNo[i].id = this.chartNoOptions[i].CHART_NO;
          this.chartNoOptionsIdNo[i].fullName = this.chartNoOptions[i].ID_NO;
        }
      }
    });
  });
},
  selectChange() {
    //for (let j = 0; j < this.chartNoOptions.length; j++) {
    //  if (this.dataForm.chartNo === this.chartNoOptions[j].CHART_NO) {
    //    this.dataForm.patName = this.chartNoOptions[j].PAT_NAME;
    //  }
    //}
    this.dataForm.patName=this.chartNoOptions.find(t=>t.id===this.dataForm.chartNo).fullName;
  },
```

#### 不可編輯

```html
<el-col :span="24">
  <el-form-item prop="insFeeCode" label="保險說明">
    {{ dataForm.insFeeCode | dynamicText(insFeeCodeOptions) }}
  </el-form-item>
</el-col>

<el-col :span="24">
  <el-form-item prop="insFeeCode" label="保險說明">
    {{ dataForm.insFeeCode }}
  </el-form-item>
</el-col>
```



# 其他

- 標題

  ```html
  <el-col :span="24">
    <groupTitle content="維護資料"/>
  </el-col>
  ```

- 日期

  ```html
  <el-date-picker
  	v-model="query.opdDate"
  	type="date"
  	placeholder="請選擇"
  	value-format="timestamp"
  	format="yyyy-MM-dd"
  />
  ```

- btn group

  ```html
  <el-button-group style="width: 100%">
    <el-tooltip effect="light" content="新增目錄" placement="bottom">
      <el-button
                 plain
                 size="mini"
                 icon="ym-custom el-icon-folder-add"
                 class="emrfrequent-btn-panel"
                 @click="addTreeItem"
                 />
    </el-tooltip>
    <el-tooltip effect="light" content="編輯目錄" placement="bottom">
      <el-button
                 plain
                 size="mini"
                 icon="ym-custom el-icon-edit"
                 class="emrfrequent-btn-panel"
                 @click="EditTreeItem"
                 :disabled="isTreeTop"
                 />
    </el-tooltip>
  
  </el-button-group>
  ```

- filter

  ```vue
  {{ scope.row.feeCode | dynamicText(feeCodeOptions) }}
  ```




# 複製Object

> 應用場景：使用物件儲存資料時，為了判斷數據是否被更動過，有不能更動的A(異動前資料)、和可以被更動的B

需要將 A 物件的值複製給 B 物件時不能直接 `this.B = this.A` 或 `this.B = {...this.A}`

上述兩種方式都是**淺拷貝**，因為指向同一塊記憶體，在vue中會導致只用v-model綁定了 B、並只對 B 進行操作，但 A 的值會跟著被更動

==解決方式==：`this.B = JSON.parse(JSON.stringify(this.A))` (深拷貝)

> **深拷貝**在複製物件時，會獨立出來不共用同一個記憶體位置，改動 `newObject` 時不會動到 `oldObject`。





# 動態更新綁定值，view無法更新

使用 `objName.newAttribute = newValue` 的方法可能導致view無法即時更新

==解決方式==：`this.$set(objName, 'newAttribute', newValue)`





# js-判斷大小寫

```js
let text = 'A';

IsUpper(code) {
  return code === code.toUpperCase()
},
  
console.log(this.IsUpper(text)); // ture
```



# js-判斷含有特定字串 indexOf

```js
let text = "there's something wrong";

console.log(text.indexOf("something") >= 0); // true
```



# js-取代特定字串 replace

```js
let text = "there's something wrong";

text.replace("something", "hahaha");

console.log(text); //there's hahaha wrong
```



# js-分割字串 split

```js
let text = "A,B,C,D";

let list = text.split(",");

// list = ["A","B","C","D"]
```

