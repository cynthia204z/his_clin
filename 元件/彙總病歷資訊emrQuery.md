# 彙總病歷查詢 EmrQueryMainPage

```vue
<EmrQueryMainPage
  fromExtraSystem
  :fromExtraSystemPatientData="patInfo"
  activePanel="1010"
  scenesCode="OERDOC"
/>
```

```js
import EmrQueryMainPage from "@/views/his7/emrquery/emrquerymainpage"
```

## 屬性

- fromExtraSystem：是否從外部掛載 EmrQueryMainPage，`true`的話不顯示search-box
- fromExtraSystemPatientData：病患資訊，fromExtraSystem為`true`時需提供
- activePanel：選中標籤頁
- scenesCode：場景代碼，帶入場景時不顯示search-box右側場景選擇