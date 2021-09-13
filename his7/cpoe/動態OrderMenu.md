# ORDER_MENU

`select * from EMR_XMLSTRUCTURE where XML_SUB_TYPE_NCID = 'ORDER_MENU';`

```js
XML_TYPE_NCID = 'EMR_ORDER'

XML_SUB_TYPE_NCID = 'ORDER_MENU'

OWNER_NCID = (orderSys)
  
//
FILLER_SYS_NCID = 'M'
```

> ==HIS3對應目前靜態HIS7==：
>
> searchOrderDialog(外層)：
>
> - menubar-id = tabsOptions.name
> - menubar-label = tabsOptions.label
>
> searchDialog(內層)：
>
> - tabsOptions.name = orderSys
>
> - tag name = pageType
> - id(orderType) = index
> - label = label
> - usageOei = invisible



## 原始 XML_CONTENT 轉 json格式

json參考格式

```json
{
  "label":"科常用(檢查檢驗)",
  "xmlSubTypeNcid":"EXAM",
  "nodeId":"-1",
  "children":[
    {
      "label":"檢查目錄",
      "nodeId":"OEN1630404581304_deptTest30000",
      "children":[]
    }
  ]
}
```



### ICD10

OWNER_NCID = 'ICD10'

XML_NAME = 'ICD10'

DISPLAY_SEQ = 1

XML_CONTENT：

```xml
<menubar id="ICD10" label="ICD10" usageOei="A">
    <doc id="DOC" label="醫師常用" usageOei="A" columnCount="2"/>    
    <dept id="Dept" label="科常用" usageOei="A" columnCount="2"/>
    <icd10CMDept id="ICD10CMDept" label="健保科常用(CM)" usageOei="A" columnCount="3"/>
    <node id="ICD10CM" label="ICD10CM(全)" usageOei="A" columnCount="2"/>
    <search id="Search" label="ICD10CM搜尋" usageOei="A" columnCount="3"/>
    <icd10PCSDept id="ICD10PCSDept" label="健保科常用(PCS)" usageOei="A" columnCount="3"/>
    <icd10PCS id="ICD10PCS" label="ICD10PCS搜尋" usageOei="A" columnCount="2"/>
</menubar>
```

```json
{"id":"ICD10","label":"ICD10","usageOei":"A","menu":[{"pageType":"freqTreeBox","id":"DOC","label":"醫師常用","usageOei":"A"},{"pageType":"freqTreeBox","id":"Dept","label":"科常用","usageOei":"A"},{"pageType":"icd10DeptBox","id":"ICD10CMDept","label":"健保科常用(CM)","usageOei":"A"},{"pageType":"treeSearchBox","id":"ICD10CM","label":"ICD10CM(全)","usageOei":"A"},{"pageType":"searchBox","id":"Search","label":"ICD10CM搜尋","usageOei":"A"},{"pageType":"icd10DeptBox","id":"ICD10PCSDept","label":"健保科常用(PCS)","usageOei":"A"},{"pageType":"icd10PCSSearchBox","id":"ICD10PCS","label":"ICD10PCS搜尋","usageOei":"A"}]}
```



### PHM

OWNER_NCID = 'PHM'

XML_NAME = '藥囑'

DISPLAY_SEQ = 2

XML_CONTENT：

```xml
<menubar id="PHM" label="藥囑" usageOei="A">
	<doc id="DOC" label="醫師常用" usageOei="A" columnCount="2"/>
	<dept id="Dept" label="科常用" usageOei="A" columnCount="2"/>
	<node id="PHM" label="藥品" usageOei="A" columnCount="2"/>
	<search id="Search" label="搜尋(全部)" usageOei="A" columnCount="3"/>
	<search id="Search" label="搜尋(常備)" usageOei="A" columnCount="3" criterion="='1'"/>   
	<search id="Search" label="搜尋(非常備)" usageOei="A" columnCount="3" criterion="!='1'"/>
</menubar>
```

```json
{"id":"PHM","label":"藥囑","usageOei":"A","menu":[{"pageType":"freqTreeBox","id":"DOC","label":"醫師常用","usageOei":"A"},{"pageType":"freqTreeBox","id":"Dept","label":"科常用","usageOei":"A"},{"pageType":"treeSearchBox","id":"PHM","label":"藥品","usageOei":"A"},{"pageType":"searchBox","id":"Search","label":"搜尋(全部)","usageOei":"A"},{"pageType":"searchBox","id":"phmSearchOften","label":"搜尋(常備)","usageOei":"A","criterion":"='1'"},{"pageType":"searchBox","id":"phmSearchNoOften","label":"搜尋(非常備)","usageOei":"A","criterion":"!='1'"}]}
```



### TREDEN

OWNER_NCID = 'TREDEN'

XML_NAME = '處置'

DISPLAY_SEQ = 3

XML_CONTENT：

```xml
<menubar id="TREDE" label="處置" usageOei="A">
  <doc id="DOC" label="醫師常用" usageOei="A"/>
  <dept id="Dept" label="科常用" usageOei="A"/>
  <node id="TRE" label="治療處置" usageOei="A"/>
  <node id="REH" label="復健治療" usageOei="A"/>
  <node id="CANC" label="癌症治療" usageOei="A"/>
  <node id="PSY" label="精神治療" usageOei="A"/>
  <node id="RT" label="呼吸治療" usageOei="A"/>
  <search id="Search" label="搜尋" usageOei="A"/>
</menubar>
```

```json
{"id":"TREDEN","label":"處置","usageOei":"A","menu":[{"pageType":"freqTreeBox","id":"DOC","label":"醫師常用","usageOei":"A"},{"pageType":"freqTreeBox","id":"Dept","label":"科常用","usageOei":"A"},{"pageType":"treeSearchBox","id":"TRE","label":"治療處置","usageOei":"A"},{"pageType":"treeSearchBox","id":"REH","label":"復健治療","usageOei":"A"},{"pageType":"treeSearchBox","id":"CANC","label":"癌症治療","usageOei":"A"},{"pageType":"treeSearchBox","id":"PSY","label":"精神治療","usageOei":"A"},{"pageType":"treeSearchBox","id":"RT","label":"呼吸治療","usageOei":"A"},{"pageType":"searchBox","id":"Search","label":"搜尋","usageOei":"A"}]}
```



### EXAM

OWNER_NCID = 'EXAM'

XML_NAME = '檢驗檢查'

DISPLAY_SEQ = 4

XML_CONTENT：

```xml
<menubar id="EXAM" label="檢驗檢查" usageOei="A">
    <doc id="DOC" label="醫師常用" usageOei="A"/>
    <dept id="Dept" label="科常用" usageOei="A"/>
    <oth id="16F" label="16樓檢查" usageOei="A"/>
    <node id="EXAM" label="檢查" usageOei="A"/>
    <node id="LAB" label="檢驗" usageOei="A"/>
    <node id="PAHO" label="病理" usageOei="A"/>
    <node id="XRAY" label="放射" usageOei="A"/>
    <node id="NME" label="核醫(PET)" usageOei="A"/>
    <oth id="DNATest" label="基因檢測" usageOei="A"/>
    <search id="Search" label="搜尋" usageOei="A"/>
</menubar>
```

```json
{"id":"EXAM","label":"檢驗檢查","usageOei":"A","menu":[{"pageType":"freqTreeBox","id":"DOC","label":"醫師常用","usageOei":"A"},{"pageType":"freqTreeBox","id":"Dept","label":"科常用","usageOei":"A"},{"pageType":"treeSearchBox","id":"16F","label":"16樓檢查","usageOei":"A"},{"pageType":"treeSearchBox","id":"EXAM","label":"檢查","usageOei":"A"},{"pageType":"treeSearchBox","id":"LAB","label":"檢驗","usageOei":"A"},{"pageType":"treeSearchBox","id":"PAHO","label":"病理","usageOei":"A"},{"pageType":"treeSearchBox","id":"XRAY","label":"放射","usageOei":"A"},{"pageType":"treeSearchBox","id":"NME","label":"核醫(PET)","usageOei":"A"},{"pageType":"treeSearchBox","id":"DNATest","label":"基因檢測","usageOei":"A"},{"pageType":"searchBox","id":"Search","label":"搜尋","usageOei":"A"}]}
```



### ORAN

OWNER_NCID = 'ORAN'

XML_NAME = '手術麻醉'

DISPLAY_SEQ = 5

XML_CONTENT：

```xml
<menubar id="ORAN" label="手術麻醉" usageOei="A">
    <doc id="DOC" label="醫師常用" usageOei="A"/>
    <dept id="Dept" label="科常用" usageOei="A"/>
    <node id="OR" label="全院手術" usageOei="A"/>
    <node id="OPA" label="手術設備" usageOei="A"/>
    <node id="OPM" label="手術衛材" usageOei="A"/>
    <node id="AN" label="麻醉" usageOei="A"/>
    <search id="Search" label="搜尋" usageOei="A"/>
</menubar>
```

```json
{"id":"ORAN","label":"手術麻醉","usageOei":"A","menu":[{"pageType":"freqTreeBox","id":"DOC","label":"醫師常用","usageOei":"A"},{"pageType":"freqTreeBox","id":"Dept","label":"科常用","usageOei":"A"},{"pageType":"treeSearchBox","id":"OR","label":"全院手術","usageOei":"A"},{"pageType":"treeSearchBox","id":"OPA","label":"手術設備","usageOei":"A"},{"pageType":"treeSearchBox","id":"OPM","label":"手術衛材","usageOei":"A"},{"pageType":"treeSearchBox","id":"AN","label":"麻醉","usageOei":"A"},{"pageType":"searchBox","id":"Search","label":"搜尋","usageOei":"A"}]}
```



### MTRL

OWNER_NCID = 'MTRL'

XML_NAME = '衛材'

DISPLAY_SEQ = 6

XML_CONTENT：

```xml
<menubar id="MTRL" label="衛材" usageOei="A">
    <doc id="DOC" label="醫師常用" usageOei="A" columnCount="2"/>
    <dept id="Dept" label="科常用" usageOei="A" columnCount="2"/>
    <search id="Search" label="搜尋" usageOei="A" columnCount="3"/>
</menubar>
```

```json
{"id":"MTRL","label":"衛材","usageOei":"A","menu":[{"pageType":"freqTreeBox","id":"DOC","label":"醫師常用","usageOei":"A"},{"pageType":"freqTreeBox","id":"Dept","label":"科常用","usageOei":"A"},{"pageType":"searchBox","id":"Search","label":"搜尋","usageOei":"A"}]}
```



### PKG

OWNER_NCID = 'PKG'

XML_NAME = '套餐'

DISPLAY_SEQ = 7

XML_CONTENT：

```xml
<menubar id="PKG" label="套餐" usageOei="A">
    <doc id="DOC" label="醫師套餐" usageOei="A"/>
    <dept id="Dept" label="科套餐" usageOei="A"/>
    <drg id="Drg" label="臨床路徑套餐3.4" usageOei="I"/>
    <drg id="Drg40" label="臨床路徑套餐4.0" usageOei="I"/>
</menubar>
```

```json
{"id":"PKG","label":"套餐","usageOei":"A","menu":[{"pageType":"freqTreeBox","id":"DOC","label":"醫師套餐","usageOei":"A"},{"pageType":"freqTreeBox","id":"Dept","label":"科套餐","usageOei":"A"},{"pageType":"drg","id":"Drg","label":"臨床路徑套餐3.4","usageOei":"I"},{"pageType":"drg","id":"Drg40","label":"臨床路徑套餐4.0","usageOei":"I"}]}
```



### OTH

OWNER_NCID = 'OTH'

XML_NAME = '其它'

DISPLAY_SEQ = 8

XML_CONTENT：

```xml
<menubar id="OTH" label="其它" usageOei="A">
	<doc id="DOC" label="醫師常用" usageOei="A"/>
	<dept id="Dept" label="科常用" usageOei="A"/>
	<node id="RT" label="呼吸治療" usageOei="A"/>
	<node id="HMO" label="洗腎" usageOei="A"/>
	<node id="BLD" label="血庫" usageOei="A"/>
	<node id="AH" label="預防保健" usageOei="O"/>
	<node id="VIT" label="Vital Sign" usageOei="IE"/>
	<node id="DIE" label="營養品" usageOei="IO"/>
	<node id="AGR" label="同意書" usageOei="A"/>
	<node id="GMS" label="庶務費" usageOei="A"/>
	<node id="MCC" label="醫美" usageOei="O"/>
	<node id="HC" label="居家" usageOei="O"/>
	<node id="INJ" label="注射技術費" usageOei="O"/>
	<search id="Search" label="搜尋" usageOei="A"/>
</menubar>
```

```json
{"id":"OTH","label":"其它","usageOei":"A","menu":[{"pageType":"freqTreeBox","id":"DOC","label":"醫師常用","usageOei":"A"},{"pageType":"freqTreeBox","id":"Dept","label":"科常用","usageOei":"A"},{"pageType":"treeSearchBox","id":"RT","label":"呼吸治療","usageOei":"A"},{"pageType":"treeSearchBox","id":"HMO","label":"洗腎","usageOei":"A"},{"pageType":"treeSearchBox","id":"BLD","label":"血庫","usageOei":"A"},{"pageType":"treeSearchBox","id":"AH","label":"預防保健","usageOei":"O"},{"pageType":"treeSearchBox","id":"VIT","label":"Vital Sign","usageOei":"IE"},{"pageType":"treeSearchBox","id":"DIE","label":"營養品","usageOei":"IO"},{"pageType":"treeSearchBox","id":"AGR","label":"同意書","usageOei":"A"},{"pageType":"treeSearchBox","id":"GMS","label":"庶務費","usageOei":"A"},{"pageType":"treeSearchBox","id":"MCC","label":"醫美","usageOei":"O"},{"pageType":"treeSearchBox","id":"HC","label":"居家","usageOei":"O"},{"pageType":"treeSearchBox","id":"INJ","label":"注射技術費","usageOei":"O"},{"pageType":"searchBox","id":"Search","label":"搜尋","usageOei":"A"}]}
```



### NOTE

OWNER_NCID = 'NOTE'

XML_NAME = 'Note'

DISPLAY_SEQ = 9

XML_CONTENT：

```xml
<menubar id="NOTE" label="Note" usageOei="EI">
    <doc id="DOC" label="醫師常用" usageOei="A"/>
    <dept id="Dept" label="科常用" usageOei="A"/>
    <hosp id="HOSP" label="全院常用" usageOei="A"/>
</menubar>
```

```json
{"id":"NOTE","label":"Note","usageOei":"EI","menu":[{"pageType":"freqTreeBox","id":"DOC","label":"醫師常用","usageOei":"A"},{"pageType":"freqTreeBox","id":"Dept","label":"科常用","usageOei":"A"},{"pageType":"hosp","id":"HOSP","label":"全院常用","usageOei":"A"}]}
```



### DITTO

OWNER_NCID = 'DITTO'

XML_NAME = 'DITTO'

DISPLAY_SEQ = 0

XML_CONTENT：

```xml
<menubar id="DITTO" label="DITTO" usageOei="EI">
    <ditto id="O" label="門診" usageOei="A" columnCount="2"/>
    <ditto id="E" label="急診" usageOei="A" columnCount="2"/>
    <ditto id="I" label="住院" usageOei="A" columnCount="2"/>
</menubar>
```

```json
{"id":"DITTO","label":"DITTO","usageOei":"EI","menu":[{"pageType":"ditto","id":"O","label":"門診","usageOei":"A"},{"pageType":"ditto","id":"E","label":"急診","usageOei":"A"},{"pageType":"ditto","id":"I","label":"住院","usageOei":"A"}]}
```



### ICD9

OWNER_NCID = 'ICD9'

XML_NAME = 'ICD9'

DISPLAY_SEQ = 20

XML_CONTENT：

```xml
<menubar id="ICD9" label="ICD9" usageOei="A">
  <doc id="DOC" label="醫師常用" usageOei="A" columnCount="2"/>
  <icdDoc id="icdDoc" label="住院ICD9" usageOei="I" columnCount="3"/>
  <dept id="Dept" label="科常用" usageOei="A" columnCount="2"/>
  <node id="ICD" label="ICD9" usageOei="A" columnCount="2"/>
  <search id="Search" label="搜尋" usageOei="A" columnCount="3"/>
</menubar>
```

```json
{"id":"ICD9","label":"ICD9","usageOei":"A","menu":[{"pageType":"freqTreeBox","id":"DOC","label":"醫師常用","usageOei":"A"},{"pageType":"icdDoc","id":"icdDoc","label":"住院ICD9","usageOei":"I"},{"pageType":"freqTreeBox","id":"Dept","label":"科常用","usageOei":"A"},{"pageType":"treeSearchBox","id":"ICD","label":"ICD9","usageOei":"A"},{"pageType":"searchBox","id":"Search","label":"搜尋","usageOei":"A"}]}
```



### NIS_ORDER

OWNER_NCID = 'NIS_ORDER'

XML_NAME = '補開立緊急醫囑'

DISPLAY_SEQ = 30

XML_CONTENT：

```xml
<menubar id="NIS_ORDER" label="補開立緊急醫囑" usageOei="I">
    <nisOrder id="NIS_ORDER" label="緊急醫囑" usageOei="A" columnCount="3"/>
</menubar>
```

```json
{"id":"NIS_ORDER","label":"補開立緊急醫囑","usageOei":"I","menu":[{"pageType":"nisOrder","id":"NIS_ORDER","label":"緊急醫囑","usageOei":"A"}]}
```



# 其他 XML_TYPE_NCID

```sql
--XML_TYPE_NCID:
--DOC_ORDER_FREQUENT //醫師常用
--DEPT_ORDER_FREQUENT //科常用
--DOC_ORDER_PKG //醫師套餐
--DEPT_ORDER_PKG //科套餐

select XML_SUB_TYPE_NCID, XML_TYPE_NCID, OWNER_NCID, XML_NAME
from EMR_XMLSTRUCTURE
where XML_TYPE_NCID != 'DOC_ORDER_FREQUENT'
  and XML_TYPE_NCID != 'DEPT_ORDER_FREQUENT'
  and XML_TYPE_NCID != 'DOC_ORDER_PKG'
  and XML_TYPE_NCID != 'DEPT_ORDER_PKG'
  and XML_TYPE_NCID != 'EMR_ORDER'
  
--HOST_ORDER_FREQUENT //全院常用(Note)
--DRG_ORDER_PKG //DRG套餐
--DRG40_ORDER_PKG //DRG套餐
--OTH_ORDER_FREQUENT //16樓檢查中心、基因檢測
--ORDER_XML //OR XML
--DOC_TEACH_FREQUENT //醫師常用(衛教)
--DEPT_TEACH_FREQUENT //科常用(衛教)
```
