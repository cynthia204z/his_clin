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



# 企業組件

## List EditPage

### ReadOnly

```vue
		<el-table-column prop="oeiType" label="來源" align="left" show-overflow-tooltip
                     v-if="showColumns.find(item=>item.prop === 'oeiType')"
    ></el-table-column>
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

