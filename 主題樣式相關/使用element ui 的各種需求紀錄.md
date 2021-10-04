# el-table

## 表頭插槽

```html
<el-table>
  <el-table-column>
    <template v-slot:header></template>
  </el-table-column>
</el-table>
```

## 行尾插槽

```html
<el-table>
  <el-table-column></el-table-column>
  <el-table-column></el-table-column>
  <template v-slot:append></template>
</el-table>
```

### 與其他功能一起使用時需要解決的各種問題

固定列覆蓋

## 自動滾動至表尾