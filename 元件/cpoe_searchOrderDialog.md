# searchOrderDialog  開立(手術麻醉),開立(ICD10)

ICD10: ICD10
藥囑: PHM
處置: TREDEN
檢驗檢查: EXAM
手術麻醉: ORAN
衛材: MTRL
套餐: PKG
其他: OTH

```vue
<searchOrderDialog
      :searchOrderDialogVisible="popup.searchOrderDialogVisible"
      :info="docInfo"
      :patInfo="patInfo"
      :orderSys="orderSys"
      :showList="showList"
      @close="popup.searchOrderDialogVisible = false"
      @bringItemsBack="bringItemsBack"
></searchOrderDialog>
```

```js
import searchOrderDialog from '@/views/his7/emr/cpoe/dialog/searchOrderDialog'

export default{
  data(){
    return{
      docInfo: {
        docCode: '', // 醫師代碼(醫師常用使用)
        deptCode: '', // 科別代碼(科常用使用)
      },
      popup: {
        searchOrderDialogVisible: false
      },
      
      //ICD10:ICD10, 手術麻醉:ORAN
      orderSys: 'ICD10',// 開啟視窗時選中的醫囑類別

      //各UI自訂要顯示的醫囑類別，如果設定此屬性則不判斷菜單本身的usageOei和UI傳入的usageOei
      showList: {
        ICD10: true,
        // ORAN: true
      }
    }
  },
  methods: {
    bringItemsBack(itemList){
      //itemList帶回的項目
    }
  }
}
```

# insCodeToPcsDialog 健保碼轉換 ICD10PCS

```vue
<insCodeToPcsDialog
      :ICD10PCSSearchDialogVisible="popup.ICD10PCSSearchDialogVisible"
      :info="docInfo"
      @close="closeSearchICS10PCSDialog"
      @bringItemsBack="bringItemsBack"
      :append-to-body="true"
></insCodeToPcsDialog>
```

```js
import insCodeToPcsDialog from '@/views/his7/emr/cpoe/dialog/InsCodeToPcsDialog'
// info, bringItemsBack同searchOrderDialog
```

