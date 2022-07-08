# JNPF Note

## 不顯示在菜單中的分頁

1. 在菜單管理中註冊此頁面，不顯示

2. 開啟新分頁並傳參

   ```js
   // query: 參數
   this.$router.push({ path: '/his7/emr/ierpat/view/IerMainPage', query: { data: object }});
   ```

3. 動態分頁名稱

   ```js
   this.$route.meta.zhTitle = "newName"
   ```

   > 用this.$route.meta.xxxx 讀寫<b style="color:orange">當前頁面</b>的route

4. 取得傳給當前頁的參數

   ```js
   this.$route.query.data
   ```

   

## 刪除當前tag並轉跳前一個路由

```js
let data = {
  path: "/his7/emr/oerpat/view/OerMainPage"
}
this.$router.go(-1);
this.$store.commit('tagsView/DEL_VISITED_VIEW', data)
```



## 從vuex取得用戶資訊

```javascript
import { mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['userInfo']),
  },
  methods: {
    // 取得
    this.userInfo.userAccount
  }
}
```

```markdown
# 常用
- userId: 用戶id
- userAccount: 用戶帳號
- userName: 用戶姓名

# 其他
- headIcon: 用戶頭像
- departmentId: 部門主鍵
- departmentName: 部門名稱
- organizeId: 組織主鍵
- organizeName: 組織名稱
- positionIds: 崗位
- prevLogin: 上次登錄
- prevLoginTime: 上次登錄時間
- prevLoginIPAddress: 上次登錄IP
- prevLoginIPAddressName: 上次登錄地址
- portalId: 門戶id
```



## 保留跨頁/搜尋勾選狀態

狀況1：資料庫裡面有存選取狀態

```vue
<JNPFTable
  ref="List"
  :data="list"
  @selection-change="handleSelectChange">
</JNPFTable>
```

```js
/* 此範例的allSelection只有存特定欄位 */

// 1. 取得DB裡的選取狀態，賦值給 this.allSelection
// EX: this.allSelection = res.data.list[0].selectedIds
//                                           ↑ ["1", "2", "3"]

initData(){
  // 2. 取得table list
  this.list = res.data.list
 	// 3. 篩選list中的已勾選資料
	let selectionList = this.list.filter(item => this.allSelection.includes(item.id))
  this.handleSelectChange(selectionList)
  this.resetSelection()
}

// 4. 重新取得完整的selection
handleSelectChange(data) {
  // 暫存新的勾選data
  let newSelection = []
  if (data.length) {
    newSelection = data.map(item => item.id)
  }
  // 未變更的勾選data (不在list中的資料)
  let unchangedSelection = []
  this.allSelection.forEach(slc => {
    if (!this.list.find(item => slc === item.id)) {
      unchangedSelection.push(slc)
    }
  })
  // 和未篩選前的勾選項目合併
  this.allSelection = [...filterKeywordSelection, ...unchangedSelection]
}

// 重設UI上的勾選標記
resetSelection() {
  this.allSelection.forEach(slc => {
    let row = this.list.find(item => slc === item.id)
    // 當前頁存在的資料才顯示勾選
    if (row) {
      this.$nextTick(() => {
        this.$refs.List.$refs.JNPFTable.toggleRowSelection(row, true)
      })
    }
  })
}
```

狀況2：只在UI上暫存list的勾選狀態

```vue
<JNPFTable 
  ref="List"
  :data="list"
  @selection-change="handleSelectChange">
</JNPFTable>
```

```js
initData(){
  this.list = res.data.list
  let selectionList = this.custData.filter(cust => this.selection.find(slc => slc.id === cust.id))
  this.handleSelectChange(selectionList)
  this.resetSelection()
}

handleSelectChange(data) {
  let newSelection = data ? data : []
  let unchangeSelection = []
  this.selection.forEach(slc => {
    if(!this.l.find(cust => cust.id === slc.id)){
      unchangeSelection.push(slc)
    }
  })
  this.selection = [...new Set([...newSelection, ...unchangeSelection])]
}

resetSelection(){
  this.selection.forEach(slc => {
    let row = this.list.find(item => slc === item.id)
    if (row) {
      this.$nextTick(() => {
        this.$refs.List.$refs.JNPFTable.toggleRowSelection(row, true)
      })
    }
  })
}
```





# 企業組件

## List EditPage

### ReadOnly

```vue
<el-table-column prop="oeiType" label="來源" align="left" show-overflow-tooltip
                 v-if="showColumns.find(item=>item.prop === 'oeiType')">
</el-table-column>
```

### Input

```vue
<el-table-column prop="unusedReason" label="EKG超時不給PCI原因"
                 align="left"
                 show-overflow-tooltip
                 v-if="showColumns.find(item=>item.prop === 'unusedReason')"
                 width="180"
                 >
  <template slot-scope="scope">
    <span v-show="scope.row.index === cellClickIndex">
      <el-input v-model="scope.row.unusedReason"
                clearable
                :style='{"width":"100%"}'
                @focus="cellFocusEvent(scope.row)"
                @blur="cellBlurEvent(scope.row)"
                v-focus
                maxlength="100"
                >
      </el-input>
    </span>
    <span v-show="scope.row.index !== cellClickIndex">{{ scope.row.unusedReason }}</span>
  </template>
</el-table-column>
```

### CheckBox

```vue
<el-table-column prop="holidayFlag" label="假日" align="left" show-overflow-tooltip
                 v-if="showColumns.find(item=>item.prop === 'holidayFlag')">
  <template slot-scope="scope">
    <el-checkbox v-model="scope.row.holidayFlag" true-label="Y" false-label="N"
                 @change="cellBlurEvent(scope.row)">
      {{ scope.row.holidayFlag === 'Y' ? '是' : '否' }}
    </el-checkbox>
  </template>
</el-table-column>
```

### DatePicker

```vue
<el-table-column prop="tropiDate" label="開Trop時間"
                 align="left"
                 show-overflow-tooltip
                 v-if="showColumns.find(item=>item.prop === 'tropiDate')"
                 width="130"
                 >
  <template slot-scope="scope">
    <span v-show="scope.row.index === cellClickIndex">
      <el-date-picker v-model="scope.row.tropiDate"
                      clearable
                      :style='{"width":"100%"}'
                      type="datetime"
                      format="yyyy-MM-dd HH:mm"
                      value-format="yyyy-MM-dd HH:mm"
                      @focus="cellFocusEvent(scope.row)"
                      @blur="cellBlurEvent(scope.row)"
                      maxlength="100"
                      >
      </el-date-picker>
    </span>
    <span v-show="scope.row.index !== cellClickIndex">{{ scope.row.tropiDate }}</span>
  </template>
</el-table-column>
```

### Button

```vue
<el-table-column label="預覽" align="left" fixed width="65">
  <template slot-scope="scope">
    <el-button type="text">病歷</el-button>
  </template>
</el-table-column>
```

### Select

```vue
<el-table-column prop="confirmFlag" label="確認註記"
                 align="left"
                 show-overflow-tooltip
                 v-if="showColumns.find(item=>item.prop === 'confirmFlag')"
                 fixed
                 width="100"
                 >
  <template slot-scope="scope">
    <span v-show="scope.row.index === cellClickIndex">
      <el-select v-model="scope.row.confirmFlag"
                 :style='{"width":"100%"}'
                 @focus="cellFocusEvent(scope.row)"
                 @blur="cellBlurEvent(scope.row, 'confirmFlag')"
                 >
        <el-option v-for="(item, index) in confirmFlagOptions"
                   :key="index"
                   :label="item.fullName"
                   :value="item.id"
                   ></el-option>
      </el-select>
    </span>
    <span v-show="scope.row.index !== cellClickIndex"
          >{{ valueFilter(scope.row.confirmFlag, confirmFlagOptions, 'id', 'fullName') }}</span>
  </template>
</el-table-column>
```



## Search

### Date

```vue
<el-col :span="6">
  <el-form-item label="健檢日期">
    <el-date-picker v-model="query.healthDate"
                    type="date"
                    format="yyyy-MM-dd"
                    value-format="yyyy-MM-dd"
                    ></el-date-picker>
  </el-form-item>
</el-col>
```

### Select

```vue
<el-select v-model="query.confirmFlag">
  <el-option v-for="(item, index) in hmspackageType"
             :key="index"
             :label="item.CODE_DESC"
             :value="item.CODE_NO"
             ></el-option>
</el-select>
```

### Input

```vue
<el-col :span="6">
  <el-form-item label="套餐簡碼">
    <el-input v-model="query.packCode" clearable></el-input>
  </el-form-item>
</el-col>
```

### PopupLov

```vue
<el-col :span="6">
  <el-form-item label="勞職/簽帳公司">
    <el-input v-model="query.customerCode" placeholder="勞職/簽帳公司" clearable>
      <template slot="append">
        <el-button slot="append"
                   icon="el-icon-search"
                   @click="choice('HmsCustomermstLov')"/>
      </template>
    </el-input>
  </el-form-item>
</el-col>
```

```vue
<PopupLov ref="HmsReportItemmstLov2"
          :lov-config="popupLovConfig.HmsReportItemmstLov2"
          @lovEvent="(data) => handlePopupLovData(data, 'itemCatalog', '')"
          />
```

```js
choice(aLovName) {
  this.$nextTick(() => {
    this.$refs[aLovName].init();
  })
}

handlePopupLovData(data, columnName, dataColumnName) {
  if (data.length > 0) {
    this.$set(this.query, columnName, data[0][dataColumnName])
    console.log(this.query[columnName])
  }
}
```

