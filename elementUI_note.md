# Element UI Note

## 共通

### 回調函數：保留組件預設參數並加上自定義參數

```vue
<el-table :data='data'
          @row-click="(row, column, event) => handelRowClick(row, column, event, 'drug')"
          ></el-table>
```

```js
handelRowClick(row, column, event, tableName){
  // do something
},
```



## CheckBox

### ture/false-value

```vue
<el-checkbox v-model="dataForm.phraseStatus" true-label="Y" false-label="N"></el-checkbox>
```



## DatePicker

### 可選範圍: picker-options

```vue
<el-date-picker v-model="dataForm.orderStartDate"
                value-format="yyyy-MM-dd"
                :picker-options="datePickerOptions"
                ></el-date-picker>
```

```js
export default{
  data(){
    return{
      // 包含今天的未來一週
      datePickerOptions: {
        disabledDate(time) {
          const date = new Date()
          date.setTime(date.getTime() + 3600 * 1000 * 24 * 6)
          return time.getTime() < Date.now() - 8.64e7 || time.getTime() > date
        }
      }
    }
  } 
}
```



## Message

### 等待某事件結束後關閉

其他種類的message，如notify也可以這樣用

```js
this.waitSaveMsg = this.$message({
  duration: 0, // 加了這個才不會自動關掉
  message: '儲存中，請勿關閉視窗',
  type: 'warning'
})

saveAsynchronous().then(()=>{
  this.waitSaveMsg.close()
  this.$message.success('儲存完畢!')
})
```



## Notify

```js
this.waitSaveMsg = this.$notify({
  title: '請注意',
  message: '儲存主檔中，請勿關閉視窗',
  type: 'warning',
  duration: 0,
  showClose: false
})

saveMst().then(()=>{
  this.waitSaveMsg.message = '儲存明細中，請勿關閉視窗'
})
```



## Table

### 改表頭文字

無表頭勾選框的勾選欄位

```vue
<el-table :data="data" class="no-header-checkbox-table">
	<el-table-column type="selection" label-class-name="no-checkbox-header"></el-table-column>
</el-table>
```

```scss
.no-header-checkbox-table >>> .no-checkbox-header .cell .el-checkbox__inner{
  display: none;
  position: relative;
}
.no-header-checkbox-table >>> .no-checkbox-header .cell::before{
  content: "選取";
  position: absolute;
  
}
```



### 表頭加樹狀狀態控制

```vue
<el-table-column prop="focusDatetime" width="200" show-overflow-tooltip sortable="custom">
  <template #header>
    <el-tooltip :content="treeExpandedStatus ? '全部收起' : '全部展開'" placement="top">
      <el-button type="text" @click.stop="toggleRowExpansion">
        <em v-if="treeExpandedStatus" class="ym-custom ym-custom-view-list"/>
        <em v-else class="ym-custom ym-custom-file-tree"/>
      </el-button>
    </el-tooltip>
    紀錄時間
  </template>
  <template slot-scope="scope">
    <span class="font-color-1">{{ scope.row.focusDatetime }}</span>
  </template>
</el-table-column>
```

```js
// 樹狀展開/收起全部
toggleRowExpansion(){
  this.treeExpandedStatus = !this.treeExpandedStatus
  this.list.forEach(row => {
    this.$refs.table.$refs.JNPFTable.toggleRowExpansion(row, this.treeExpandedStatus)
  })
}
```



### 樹狀合併儲存格

```vue
<JNPFTable :data="list"
           v-loading="false"
           :hasNO="false"
           highlight-current-row
           @current-change="handleCurrentChange"
           @expand-change="handleExpandChange"
           class="bottom-line"
           size="mini"
           @sort-change="handleSortChange"
           :span-method="objectSpanMethod"
           :row-key="(row) => {return row.id + row.itemOrder + row.isFirstrow}"
           :tree-props="{children: 'children', hasChildren: ''}"
           default-expand-all
           ref="table"
           >
  <el-table-column prop="focusDatetime" label="紀錄時間" width="200" show-overflow-tooltip sortable="custom"></el-table-column>
  <el-table-column prop="sheetName" label="焦點名稱" width="180" show-overflow-tooltip></el-table-column>
  <el-table-column prop="itemDart" label="類別" width="60" align="center">
    <template slot-scope="scope">
      {{scope.row.expanded ? scope.row.itemDart: ''}}
    </template>
  </el-table-column>
  <el-table-column prop="itemContent" label="紀錄內容" min-width="300" show-overflow-tooltip>
    <template slot-scope="scope">
      {{scope.row.expanded ? scope.row.itemContent: ''}}
    </template>
  </el-table-column>
  <el-table-column prop="focusRecorderName" label="紀錄者" width="80" show-overflow-tooltip>
    <template slot-scope="scope">
      {{scope.row.expanded ? scope.row.focusRecorderName: ''}}
    </template>
  </el-table-column>
</JNPFTable>
```

```js
export default {
  data() {
    return {
      // 合併依據
      spanArr: [],
      // UI上的變平數據
      flatListAll: []
    }
  },
  created() {
    this.initData()
  },
  methods: {
    initData() {
      postData(uiDoGetPatFocusSheetItemList, this.query).then(res => {
        this.list = res.data
        this.list.forEach(item => this.handleExpandChange(item, true))
        this.flatList()
        this.flitterData()
      })
    },
    // 合併儲存格方法
    objectSpanMethod({ row, column, rowIndex, columnIndex }) {
      if (columnIndex === 0 || columnIndex === 1) {
        console.warn(row.expanded, row.isFirstrow, rowIndex, this.spanArr[rowIndex])
        if (this.spanArr[rowIndex] && row.expanded) {
          return {
            rowspan: this.spanArr[rowIndex],
            colspan: 1
          }
        } else if(row.isFirstrow === 'Y'){
          return {
            rowspan: 1,
            colspan: 1
          }
        }else{
          return {
            rowspan: 0,
            colspan: 0
          }
        }
      }
    },
    // 合併設定
    flitterData() {
      if (!this.list.length) {
        this.spanArr = []
        return
      }
      let flatList = this.flatListAll
      let spanArr = []
      let contactDot = 0
      flatList.forEach((item, index) => {
        if (index === 0) {
          spanArr.push(1)
        } else {
          let current = item.id
          let next = flatList[index - 1].id
          if (current === next) {
            spanArr[contactDot] += 1
            spanArr.push(0)
          } else {
            contactDot = index
            spanArr.push(1)
          }
        }
      })
      this.spanArr = spanArr
      console.warn(spanArr)
    },
    // 資料扁平化
    flatList() {
      let list = JSON.parse(JSON.stringify(this.list))
      list.forEach(row => {
        if (row.children && row.children.length) {
          row.children.unshift(row)
        } else {
          row.children = []
        }
      })
      this.flatListAll = list.map(row => row.children).flat()
    },
    // 樹狀行展開狀態變更
    handleExpandChange(row, expanded) {
      this.list.forEach(listRow => {
        if (listRow.id === row.id) {
          listRow.expanded = expanded
          if (listRow.children && listRow.children.length) {
            listRow.children.forEach(child => child.expanded = expanded)
          }
        }
      })
      this.flatList()
      this.flitterData()
    }
  }
}
```





# Element UI： His7應用

## 可關閉可新增的標籤頁

(jnpf-web/his7/emr/ierpat/view/EmrQueryWardRoundsPage)

```vue
<el-tabs
         style="height:calc(100% - 52px)"
         v-model="tabsListActive"
         type="border-card"
         class="JNPF-el_tabs _tabs"
         @tab-remove="removeTab"
         @tab-click="clickTab"
         >
  <el-tab-pane
               :closable="false"
               class="JNPF-common-layout"
               style="width: 100%; background: #fff"
               label="病患清單"
               name="patList"
               v-loading="listLoading"
               >
  </el-tab-pane>
  <el-tab-pane
               closable
               lazy
               class="JNPF-common-layout"
               style="width: 100%; background: #fff"
               v-for="(item, index) in tabsList"
               :key="item.name"
               :index="index"
               :label="item.title"
               :name="item.name"
               >
  </el-tab-pane>
</el-tabs>
```

```js
export default {
  data() {
    return {
      patCardList: [],
      patCardListIsShow: [],
    }
  },
  methods: {
    addTab(data) {
      let targetName = 'patTPR_' + data.patName + moment()
      this.tabsList.push({
        title: `${data.patName} ${data.bedNo}`,
        name: targetName,
        data: data
      })
      this.tabsListActive = targetName
      this.patData = data
    },
    removeTab(targetName) {
      let tabs = this.tabsList
      let activeName = this.tabsListActive
      if (activeName === targetName) {
        tabs.forEach((tab, index) => {
          if (tab.name === targetName) {
            let nextTab = tabs[index + 1] || tabs[index - 1]
            if (nextTab) {
              activeName = nextTab.name
            } else {
              activeName = 'patList'
            }
          }
        })
      }
      this.tabsListActive = activeName
      this.tabsList = tabs.filter((tab) => tab.name !== targetName)
    },
    clickTab(target) {
      this.tabsList.forEach(t => {
        if (t.name === target.name) {
          this.patData = t.data
        }
      })
    }
  }  
}

```



## MENU+TABS

(jnpf-web/his7/emr/ierpat/view/IerMainPage)

```vue
<!--index.vue menu-->
<el-menu
         :default-active="activeIndex"
         class="el-menu-demo bg-color-3 selector"
         mode="horizontal"
         menu-trigger="hover"
         @select="menuSelect"
         style="display:flex"
         >
  <div v-for="(item, index) in menuOptions" :key="index">
    <el-submenu v-if="item.children" class="submenu" :index="item.name">
      <template slot="title">{{ item.title }}</template>
      <template v-for="subitem in item.children">
        <el-menu-item
                      class="hover-font-color-3 bg-color-2"
                      style="height: 30px !important; line-height: 30px !important;"
                      :index="subitem.name">
          {{ subitem.title }}
        </el-menu-item>
        <el-divider class="menu-divider" v-if="subitem.hasDivider"></el-divider>
      </template>
    </el-submenu>
    <el-menu-item v-if="!item.children" :index="item.name">{{ item.title }}</el-menu-item>
  </div>
</el-menu>
```

```vue
<!--index.vue tabs-->
<el-tabs
         v-model="editableTabsValue"
         type="border-card"
         class="JNPF-el_tabs _tabs"
         closable
         @tab-remove="removeTab"
         @tab-click="clickTab"
         >
  <el-tab-pane
               lazy
               class="JNPF-common-layout"
               style="width: 100%; background: #fff"
               v-for="(item, index) in editableTabs"
               :key="item.name"
               :index="index"
               :label="item.title"
               :name="item.name"
               >
    <!-- 彙總病歷資訊、查詢檢驗報告、查詢檢查報告、查詢病歷類別 -->
    <EmrQueryMain
                  v-if="item.name.indexOf('EmrQueryMain') !== -1"
                  :fromExtraSystemPatientData="data"
                  :fromExtraSystem="true"
                  :activePanel="EmrQueryMainActivePanel"
                  ></EmrQueryMain>
    <component
               v-else
               :ref="item.name"
               :is="item.name"
               :patData="data"
               :patInfo="data"
               :docInfo="docInfo"
               :toolbar="false"
               :childDialogModal="true"
               @openIer2011="menuSelect('Ier2011')"
               @openIer2012="menuSelect('Ier2012')"
               @openComm2010="menuSelect('Comm2010')"
               @openAllergyRecord="menuSelect('Comm3020')"
               @openComm5060="menuSelect('Comm5060')"
               @openComm6010="menuSelect('Comm6010')"
               ></component>
  </el-tab-pane>
</el-tabs>
```

```js
// index.js

import { menuOptions, otherMenu } from '@/views/his7/emr/ierpat/view/IerMainPage/js/static.js'

export default {
  data() {
    return {
      editableTabsOptions: [],
      // 預設開啟的標籤頁
      editableTabs: [
        { title: '一般處方', name: 'Ier2010' },
        { title: '病患個人資訊', name: 'Summary' },
        { title: 'TPR資訊', name: 'EmrQueryTprInfo' }
      ],
      menuOptions
    }
  },
  created() {
    this.setEditableTabsOptions()
  },
  methods: {
    // 設定可以開啟的標籤頁
    setEditableTabsOptions() {
      menuOptions.forEach(t => {
        if (t.children) {
          t.children.forEach(c => {
            if (c.isPage) {
              this.editableTabsOptions.push(c)
            }
          })
        }
      })
      otherMenu.forEach(t => {
        this.editableTabsOptions.push(t)
      })
    },
    // 點選選單項目
    menuSelect(index, path) {
      this.activeIndex = index
      let selectItem = this.editableTabs.find((t) => t.name === index)
      if (selectItem) {
        if (selectItem.name.indexOf('EmrQueryMain') !== -1) {
          this.EmrQueryMainActivePanel = this.editableTabsOptions.find((t) => t.name === index).activePanel
        }
        this.editableTabsValue = selectItem.name
      } else {
        let newtab = this.editableTabsOptions.find((t) => t.name === index)
        if (newtab) {
          if (newtab.name.indexOf('EmrQueryMain') !== -1) {
            this.EmrQueryMainActivePanel = newtab.activePanel
          }
          this.addTab(newtab)
        }
      }
    },

    // 新增標籤頁
    addTab(targetName) {
      this.editableTabs.push({
        title: targetName.title,
        name: targetName.name
      })
      this.editableTabsValue = targetName.name
    },

    // 關閉標籤頁
    removeTab(targetName) {
      let tabs = this.editableTabs
      let activeName = this.editableTabsValue
      if (activeName === targetName) {
        tabs.forEach((tab, index) => {
          if (tab.name === targetName) {
            let nextTab = tabs[index + 1] || tabs[index - 1]
            if (nextTab) {
              activeName = nextTab.name
              this.activeIndex = nextTab.name
            }
          }
        })
      }

      this.editableTabsValue = activeName
      this.editableTabs = tabs.filter((tab) => tab.name !== targetName)
    },

    // 切換標籤頁
    clickTab(target) {
      if (target.name.indexOf('EmrQueryMain') !== -1) {
        this.EmrQueryMainActivePanel = this.editableTabsOptions.find((t) => t.name === target.name).activePanel
      }
      let currentItem = this.editableTabs.find(t => t.name === target.name)
      this.activeIndex = currentItem.name
    }
  }
}
```

```js
// static.js

const menuOptions = [
  {
    title: '臨床資訊',
    name: '1',
    children: [
      {
        title: 'TPR資訊',
        name: 'EmrQueryTprInfo',
        isPage: true
      },
      {
        title: '彙總病歷資訊',
        name: 'EmrQueryMain',
        activePanel: 'emrquery1010',
        isPage: true
      },
    ]
  },
  {
    title: '處方輸入',
    name: '2',
    children: [
      {
        title: '一般處方',
        name: 'Ier2010',
        isPage: true
      },
      {
        title: '診斷維護',
        name: 'Ier2020',
        isPage: true
      },
    ]
  },
  {
    title: '病歷作業',
    name: '3',
    children: [
      {
        title: '病歷撰寫',
        name: 'DocNoteWeb'
      },
      {
        title: '病患問題管理',
        name: 'Ier1080',
        isPage: true
      },
    ]
  },
  {
    title: '病歷表單',
    name: '4',
    children: [
      {
        title: '營養風險評分',
        name: 'Ier3010'
      },
      {
        title: '加護病房營養評估表單',
        name: 'DietIcuDataView'
      },
    ]
  },
  {
    title: '其它作業',
    name: '5',
    children: [
      {
        title: '事前審查申請',
        name: 'Apy2040'
      },
      {
        title: '事前審查查詢',
        name: 'Apy3050',
        hasDivider: true
      },
    ]
  },
  {
    title: '病歷借閱',
    name: 'Ier2080'
  },
  {
    title: '雲端資料',
    name: 'cloudData'
  },
  {
    title: 'PACS系統',
    name: 'pacsLink'
  }
]

const otherMenu = [
  {
    title: '出院團隊衛教',
    name: 'Comm6010'
  },
  {
    title: '出院團隊衛教範本',
    name: 'Comm6011'
  }
]
export {
  menuOptions,
  otherMenu
}

```





