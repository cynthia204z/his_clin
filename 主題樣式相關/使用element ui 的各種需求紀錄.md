# el-table

## 固定列

#### 解決固定列覆蓋橫向滾動條

#### 解決表格錯位

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

### 與其他功能一起使用時需要解決的各種問題

#### 1. 解決固定列覆蓋表尾插槽

#### 2. 解決有橫向卷軸時表尾插槽內容跟著滾走

## 自動滾動至表尾

