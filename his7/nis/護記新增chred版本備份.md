```html
<!--    <el-button @click="getTextAndHtml">確認</el-button>-->
<!--    <chartEditor ref="chartEditor" :config="config"/>-->
```

```js
// import chartEditor from '@/components/iAlice/ChartEditor'
export default{
  data(){
    // charteditor config
    // config: {
    //   editorId: undefined,
    //   mod: 'edit',
    //   searchKind: 'SHEET',
    //   applicationMode: 'NO_FOLDER',
    //   query: {
    //     sheetType: 'Plan',
    //     ownerSys: 'NIS',
    //     encounterNo: undefined,
    //     chartNo: undefined
    //   }
    // },
    // pageName: 'nis-plan-sheet-dialog'
  },
  created() {
    // this.config.editorId = `NisPlansheetDialog_${this.caseno}`
  },
  methods: {
    // chred
    // getTextAndHtml() {
    // let data = this.$refs.chartEditor.getCheckboxPureTextAndHtml()
    // this.$emit('getPlanSheetData', data)
    // },
  }
}
```

