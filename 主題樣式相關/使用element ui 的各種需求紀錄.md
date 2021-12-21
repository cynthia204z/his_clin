# el-table

## 固定列

#### 解決固定列覆蓋橫向滾動條

子元素 z-index 比父元素高會無效，所以只好一個一個 class 挑出來強制用 pointer-events 設定

```scss
.el-table--scrollable-x .el-table__body-wrapper {
  z-index: 1;
}
.el-table__fixed-body-wrapper table {
  pointer-events: auto;
}
.el-table__fixed, .el-table__fixed-right{
  pointer-events: none;
}
.el-table thead{
  pointer-events: auto;
}
```

#### 解決表格錯位

```js
// 使用 JNPF-table
this.refs['tableRefName'].refs.JNPFTable.doLayout()
// 使用el-table
this.refs['tableRefName'].doLayout()
```

## 表頭插槽

```html
<el-table>
  <el-table-column>
    <template v-slot:header></template>
  </el-table-column>
</el-table>
```

## 表尾插槽

```html
<el-table>
  <el-table-column></el-table-column>
  <el-table-column></el-table-column>
  <template v-slot:append></template>
</el-table>
```

### 【與其他功能一起使用時需要解決的各種問題】

#### 1. 解決固定列覆蓋表尾插槽

#### 2. 解決有橫向卷軸時表尾插槽內容跟著滾走

解決：取得父元素的滾動條位置，令表尾插槽內容的 left 與父元素滾動條位置相同（模擬固定浮動於左側）

```js
mounted() {
  this.tableDom1 = this.$el.querySelector(".List1 .el-table__body-wrapper");
  this.tableDom1.addEventListener("scroll", () => {
    this.listScrollLeft1 = this.tableDom1.scrollLeft;
    let lovSelect1 = this.$refs.lovSelect1.$el;
    lovSelect1.style.left = this.listScrollLeft1 + "px";
  });
},
```

#### 3. 解決有橫向滾動條時表尾插槽容器遮擋子元素

```scss
.JNPF-common-table >>> .el-table__append-wrapper{
  overflow: visible;
}
```

#### 4. 無資料時顯示在表格頂部

問題：空資料展示圖撐開table body導致表格無資料時表尾不在頂部（而是在圖片下方）

解決：有表尾插槽時，判斷表尾區塊的兄弟元素是不是空資料展示圖，是的話代表無資料=>令圖片區塊不顯示（不是的話代表有資料）

```js
try {
  let elTableAppendWrapper = this.$el.querySelector(
    ".el-table__append-wrapper"
  );
  let elTableAppendWrapperPreviousBrotherObject =
      elTableAppendWrapper.previousElementSibling;
  if (
    elTableAppendWrapperPreviousBrotherObject ===
    this.$el.querySelector(".el-table__empty-block")
  ) {
    elTableAppendWrapperPreviousBrotherObject.style.display = "none";
  }
} catch (e) {}
```

## 自動滾動至表尾

```js
this.$nextTick(() => {
  let container = this.$el.querySelector(".el-table__body-wrapper");
  container.scrollTop = container.scrollHeight;

});
```

