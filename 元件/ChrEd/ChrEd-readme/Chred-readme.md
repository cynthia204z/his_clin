# ChratEditor使用範例

範例路徑：his7/demo/chred/chartEditor

## 組件使用注意事項

**editorId 是必填的欄位，請給一個全局的唯一固定值。**

> Chred底層的ueditor組件靠editorId來辨識當前編輯器，若全局中有兩個editorId相同的編輯器會造成渲染失敗。
>
> ※例：作業名通常不重複，可作editorId使用，如 Ier2010、nis3040、com4120 等等。
>
> ※不建議使用會更動的值來當editorId，例如：轉跳路徑重新讀取已開啟的頁面，但給的editorId和上次開啟時不同(EX: 用現在時間當ID)，可能會造成組件判斷此頁面需要渲染兩個編輯器。

## 編輯模式 mod

預設為readonly

```vue
<template>
  <div class="JNPF-common-layout">
    <div class="JNPF-common-layout-center">
      <chartEditor :config="config"/>
    </div>
  </div>
</template>

<script>
import chartEditor from '@/components/iAlice/ChartEditor'
export default {
  components: {chartEditor},
  data(){
    return{
      config: {
        editorId: 'demo-chred',
        mod: 'edit', // edit / readonly / review / trace
      }
    }
  }
}
</script>
```

## 應用模式 searchKind

預設為DEFAULT

### 應用模式一：有樹型選單

<img src="image-20220421174751150.png" alt="image-20220421174751150" style="zoom:67%;" />

```vue
<template>
  <div class="JNPF-common-layout">
    <div class="JNPF-common-layout-center">
      <chartEditor :config="config"/>
    </div>
  </div>
</template>

<script>
import chartEditor from '@/components/iAlice/ChartEditor'
export default {
  components: {chartEditor},
  data(){
    return{
      config: {
        editorId: 'demo-chred',
        mod: 'edit', 
        searchKind: 'DEFAULT', // DEFAULT / SHEET / UNIT
        query: { // 查詢參數
          encounterNo: 'I12090392', 
          chartNo: '1050888'
        }
      }
    }
  }
}
</script>
```

#### query有效欄位

searchKind=`DEFAULT`：

- encounterNo
- chartNo
- sheetId

searchKind=`SHEET`：

- encounterNo
- chartNo
- sheetType
- ownerType

searchKind=`UNIT`：

- encounterNo
- chartNo
- sheetType
- ownerType
- unit：必填

### 應用模式二：無樹型選單

<img src="image-20220421174822526.png" alt="image-20220421174822526" style="zoom:67%;" />

```vue
<template>
  <div class="JNPF-common-layout">
    <div class="JNPF-common-layout-center">
      <chartEditor :config="config"/>
    </div>
  </div>
</template>

<script>
import chartEditor from '@/components/iAlice/ChartEditor'
export default {
  components: {chartEditor},
  data(){
    return{
      config: {
        editorId: 'demo-chred',
        mod: 'edit',
        searchKind: 'ONE_SHEET', // ONE_SHEET
        query: { // 查詢參數
          encounterNo: 'I12090392',
          chartNo: '1050888'
        }
      }
    }
  }
}
</script>
```

#### query有效欄位

searchKind=`ONE_SHEET`：

- transId
- encounterNo
- chartNo
- sheetId

## 就醫序號與病歷號

存檔時會從config取得要存的就醫序號(ENCOUNTER_N)及病歷號(CHART_NO)

## 欄位和UI

### 後台

![](ChrEd病歷表單管理.png)

![image-20220614103644274](image-20220614103644274.png)

## 表單設計注意事項

設計表單插入輸入框控件時，要注意輸入框是有空間可以輸入的狀態

如下圖，如果控件變成這種無法輸入的狀態，會造成設計完成提供給前台編輯的時候無法取得控件值、無法存檔

> 除了早期設計的表單外，現在新建的表單應該比較不會遇到此問題（程式碼有debug）

![image-20220614102223297](image-20220614102223297.png)
