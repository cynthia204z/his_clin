# Vue Note

## el-table-column v-if 列位置錯亂

[element-ui el-table使用v-if來控制列的顯示隱藏 出現列位置錯亂問題](https://blog.csdn.net/weixin_45899022/article/details/103785471)

<b style="color:orange">解決方式</b>：給 el-table-column 加 `key` 屬性

EX： `<el-table-column v-if="blabla" key="1"/>` 、 `<el-table-column v-if="blabla" :key="Math.random()"/>`



## 動態更新綁定值，view無法更新

使用 `objName.newAttribute = newValue` 的方法可能導致view無法即時更新

<b style="color:orange">解決方式</b>：`this.$set(objName, 'newAttribute', newValue)`



## component標籤：動態組件

> 參考文章：
>
> https://blog.csdn.net/liangmengbk/article/details/85013547
>
> https://codesandbox.io/s/github/vuejs/vuejs.org/tree/master/src/v2/examples/vue-20-dynamic-components?file=/index.html:924-933



## 多行comfirm

```js
const h = this.$createElement
this.$confirm('提示', {
  title: '提示',
  message: h('div', [
    h('p', '第一行'),
    h('p', '第二行'),
  ]),
  confirmButtonText: '確定',
  cancelButtonText: '取消'
}).then(() => {
  // do something
}).catch(() => {
  // do something
})
```



## 在v-for中使用ref

包在迴圈裡的組件ref只會定義一個

所以要傳入index區分現在是要打開哪個標籤上的選單

```vue
<template>
<div v-for="(item, index) in arr" :key="index" @contextmenu.prevent="openMenu($event, index)">
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
        contextmenuData: [],
      };
    },
    methods: {
      openMenu(e, index) {
        // 重點
        this.$refs.contextmenu[index].openMenu(e); 
      },
      handleContextMenuClick(eventName) {},
    },
  };
</script>
```



## 在keep-alive中轉跳路由取得資料查詢

page1

```js
methods: {
gotoHms3040(){
  //取得 客戶姓名
  let lGuestChname = this.$refs.MstForm.getGuestChname()
  if (lGuestChname) {
    this.$router.push({
      path: '/his7/hms/customer/hms3040',
      query: {data: lGuestChname}
    })
  }
},
}
```

轉跳目標

```js
data(){
  return{
    //接收 link 的參數
    linkDTO: undefined,
    queryPanel04: false
  }
}

beforeRouteEnter(to, from, next){
  next((vm)=>{
    if(to.query.data){
      vm.linkDTO = to.query.data
      vm.queryPanel04 = true
    }
  })
}

watch:{
  queryPanel04(newVal){
    if(newVal){
      this.searchPanel04()
      this.queryPanel04 = false
    }
  }
}

methods: {
  searchPanel04(){
    this.$nextTick(()=>{
      this.activePane = '4'
      this.$refs.Panel04.setQueryColumn('guestChname', this.linkDTO)
    })
  }
}
```

## beforeRouteEnter

```js
beforeRouteEnter (to, from, next) {
  next(vm => {
    if(vm.$route.params && typeof vm.$route.params === 'object') {
      for (const key in vm.$route.params) {
        vm.query[key] = vm.$route.params[key]
      }
      vm.$nextTick(function() {
        vm.$refs.Search.search()
      })
    }
  })
},
```

```js
beforeRouteEnter(to, from, next) {
  next((vm) => {
    if (vm.userInfo.prevLogin == 1 && from.path == '/login') {
      //右下角提示上次登錄信息
      vm.openNotify()
    }
  })
},
```

```js
beforeRouteEnter(to, from, next){
  next((vm)=>{
    if(to.query.data){
      vm.linkDTO = to.query.data
      vm.queryPanel04 = true
    }
  })
},
```

## beforeRouteLeave

```js
beforeRouteLeave(to, from, next) {
	// do something 12345
  next()
},
```

## 選中行取消show-overflow-tooltip效果

```vue
<el-table-column  prop="hesName1" label="建議"  min-width="220" show-overflow-tooltip>
  <template slot-scope="scope">
		<span :class="{'show-all-text': currentRow && currentRow.id === scope.row.id}">{{scope.row.hesName1}}</span>
  </template>
</el-table-column>
```

```css
.show-all-text{
  white-space: break-spaces;
}
```

