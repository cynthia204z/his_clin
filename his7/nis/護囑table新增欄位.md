

## 要新增欄位的Table

NIS_PAT_BASIC

```
from EMR_IPD_ENCOUNTER where

過敏: irritation
預計出院日: planDischgDate
----------------------

治療註記:
未完成病歷:
```



OER_PATBAS_NIS_VIEW 

```
form OER_PATBAS

床位: bedNo
來源: oeiType
護理站: branchCode
----------------------

from IER_PAT_DIAG10

診斷: diagSeqFirst
----------------------
過敏: 
DRG: 
預計出院日: 

治療註記:
未完成病歷:

```

## 來源

EMR_IPD_ENCOUNTER

```sql
IRRITATION             VARCHAR2(2000 char), '過敏資訊'
PLAN_DISCHG_DATE       DATE, '預計出院日期'
DRG_CODE               VARCHAR2(20 char), 'DrgCode'

```

IER_PAT_DIAG10

> IpdpatServer\grails-app\domain\com\hcsaastech\ehis\ier\EmrIpdEncounter.groovy

```groovy
def diagRow = IerPatDiag10.find("from IerPatDiag10 where encounterNo = ? and diagSeq = '1' and diagType = 'O' and status = 'A' ", [encounterNo]);
if(diagRow != null){
  this.diagSeqFirst = diagRow.icdCode;
  this.diagSeqFirstDesc = diagRow.icdDescription;
}
```