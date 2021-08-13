**原本的LovSelect資料格式**

```html
<!-- 標籤 -->
<LovSelect
	:parent-value.sync="scope.row.chartNo"
	type="page"
  placeholder="輸入關鍵字查詢病歷號碼/姓名/身分正"
	:apiUrl="selectApi"
	:lovQueryColume="lovQueryColume"
	:lovColumeList="lovColumeList"
	optionLabel="chartNo"
	optionValue="chartNo"
	@lovEvent="lovEvent"
	@selectChange="selectChange(scope.row)"
	ref="lovSelect"
></LovSelect>
```

```json
// data()
selectApi: "/api/his7/com/chartinfo/ComChrbas",
lovQueryColume: {
  chartNo: undefined,
},
lovColumeList: [
  {
    label: "",
    content: "chartNo",
  },
  {
    label: "",
    content: "patName",
  },
  {
    label: "",
    content: "birthDate",
  },
  {
    label: "",
    content: "idNo",
  },
],
```

**換成以下寫法**

> 異動的屬性：
>
> `type、placeholder、apiUrl、lovQueryColume、lovColumeList、optionValue、(optionLabel)` =>` lovConfig`
>
> 由於呈現的文字資料已由lovColumeList設定，所以捨棄optionLabel屬性

```html
<!-- 標籤 -->
<LovSelect
	:parent-value.sync="scope.row.chartNo"
	:lovConfig="exampleLov"
	@lovEvent="lovEvent"
	@selectChange="selectChange(scope.row)"
	ref="lovSelect"
></LovSelect>
```

```json
// data()
exampleLov: {
  type: "scroll",
  placeholder: "輸入關鍵字查詢病歷號碼/姓名/身分證",
  apiUrl: "/api/his7/com/chartinfo/ComChrbas",
  lovQueryColume: {
    chartNo: undefined,
  },
  lovColumeList: [
    {
      label: "",
      content: "chartNo",
    },
    {
      label: "",
      content: "patName",
    },
    {
      label: "",
      content: "birthDate",
    },
    {
      label: "",
      content: "idNo",
    },
  ],
  optionValue: "chartNo",
},
```

