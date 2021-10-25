# 右鍵選單Contextmenu

> 範例頁：demo/rolin/contextmenu

在需要右鍵選單的標籤範圍內加入Contextmenu組件

## 例一：原生html標籤

在class為test的div內部作用

```vue
<template>
<div class="test" @contextmenu.prevent="openMenu($event)">
  <!-- div內容 -->
  <Contextmenu
               ref="contextmenu"
               :contextmenuData="contextmenuData"
               @handleContextMenuClick="handleContextMenuClick"
               ></Contextmenu>
  </div>
</template>
<script>
export default {
  data() {
    return {
      contextmenuData: [ //選項設定：title = 選項顯示文字，eventName = 事件名稱
        { title: "功能1", eventName: "event1" },
        { title: "功能2", eventName: "event2" },
        { title: "功能3", eventName: "event3" },
      ],
    };
  },
  methods: {
    openMenu(e) {
      this.$refs.contextmenu.openMenu(e); // 打開選單
    },
    handleContextMenuClick(eventName) { // 點選選項後從組件回傳事件名稱
      this[eventName](); // 觸發事件
    },
    event1() {},
    event2() {},
    event3() {},
  },
};
</script>
```

## 例二：el-form-item

要在已封裝的組件上使用的話，在組件外面包一層原生html tag是有效的

此範例的需求是在Clin-Quill組件上使用右鍵選單

> 範例頁：emr/oerpat/form/SOPform.vue

```html
<el-form-item
              label="SOP"
              prop="object"
              >
  <!--here-->
  <div @contextmenu.prevent="openMenu($event)">
    <Contextmenu
                 ref="contextmenu2"
                 :contextmenuData="contextmenuData2"
                 @handleContextMenuClick="handleContextMenuClick"
                 ></Contextmenu>
    <Clin-Quill v-model="data.object" placeholder="請輸入內容..." @pureText="getObjectText"></Clin-Quill>
  </div>
</el-form-item>
```

## 例三：JNPF-table/el-table

在table上的右鍵需求通常針對資料行，

但el-table裡面並沒有合適的slot可以放選單，所以原生html tag包在table外是一種解決方式

> **el-table**
>
> 行的右鍵事件：`@row-contextmenu`，回傳row, column, event
>
> 表頭的右鍵事件：`@header-contextmenu`，回傳column, event

```vue
<template>
<div @contextmenu.prevent="openMenu($event)">
  <JNPF-table
              :data="data"
              @row-contextmenu="getCurrentRow"
              @header-contextmenu="clearCurrentRow"
              >
    <el-table-column label="姓名" prop="name"></el-table-column>
    <el-table-column label="性別" prop="sex"></el-table-column>
    <el-table-column label="生日" prop="birth"></el-table-column>
  </JNPF-table>
  <Contextmenu
               ref="contextmenu"
               :contextmenuData="contextmenuData"
               @handleContextMenuClick="handleContextMenuClick"
               ></Contextmenu>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        data: [],
        contextmenuData: [
          { title: "功能1", eventName: "event1" },
          { title: "功能2", eventName: "event2" },
          { title: "功能3", eventName: "event3" },
        ],
        currentrow: undefined,
      };
    },
    methods: {
      openMenu(e) {
        if (this.currentrow) {
          this.$refs.contextmenu.openMenu(e);
        }
      },
      getCurrentRow(row, column, e) {// 記錄選中行
        this.currentrow = row;
      },
      clearCurrentRow(column, e) {// 如果在表頭右鍵，清空選中行
        this.currentrow = undefined;
      },
      handleContextMenuClick(eventName) {
        if (this.currentrow) {
          this[eventName]();
        }
      },
    },
  };
</script>
```

![image-20210706094052285](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/1634800039791.gif)