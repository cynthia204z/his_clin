# el-table-column v-if 列位置錯亂

[element-ui el-table使用v-if來控制列的顯示隱藏 出現列位置錯亂問題](https://blog.csdn.net/weixin_45899022/article/details/103785471)

==解決方式==：給 el-table-column 加 `key` 屬性

EX： `<el-table-column v-if="blabla" key="1"/>` 、 `<el-table-column v-if="blabla" :key="Math.random()"/>`



# 動態更新綁定值，view無法更新

使用 `objName.newAttribute = newValue` 的方法可能導致view無法即時更新

==解決方式==：`this.$set(objName, 'newAttribute', newValue)`



# component標籤：動態組件

> 參考文章：
>
> https://blog.csdn.net/liangmengbk/article/details/85013547
>
> https://codesandbox.io/s/github/vuejs/vuejs.org/tree/master/src/v2/examples/vue-20-dynamic-components?file=/index.html:924-933



# 多行comfirm

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
