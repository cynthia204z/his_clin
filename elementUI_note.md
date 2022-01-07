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





