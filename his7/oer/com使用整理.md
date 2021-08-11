## 醫囑中會用到的com

- COM_CHRBAS (病患)

- COM_DEPTBAS (科別)

- COM_DOCBAS (醫師/技術師)

- <font style="color:gray">ICD10：</font>

  COM_ICD10CM

  COM_ICD10_CHAPTER

  COM_ICD10GROUP

  COM_ICD10PCS_GROUP
  
  
  
  COM_ICD10_DEPTOFTEN_VIEW
  
  COM_ICD10CMMMP_VIEW
  
  COM_ICD10PCS_VIEW
  
  COM_ICD10PCS_DEPTOFTEN_VIEW
  
  COM_ICD10_PCSMMP_VIEW
  
  COM_ICD10_PSC_LEVEL_VIEW

![image-20210810181800069](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210810181800069.png)

- 藥囑
- 處置
- 檢驗檢查
- 手術麻醉
- 衛材
- ICD9
- 計價(?)

...



## 目前在診所版已經有用到的

- 病患

  /api/clin/com/ComChrbas

- ICD10CM國際標準碼主檔

  /api/clin/com/ComIcd10cm

- ICD10章節維護

  /api/clin/com/ComIcd10Chapter/getICD10CMOrderTreeNode

