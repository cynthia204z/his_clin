## 醫囑中用到的com

- COM_CHRBAS (病患)
- COM_DEPTBAS (科別)
- COM_DOCBAS (醫師/技術師)

1. ICD10

   - COM_ICD10CM

   - COM_ICD10_CHAPTER

   - COM_ICD10GROUP

   - COM_ICD10PCS_GROUP

   

   - COM_ICD10_DEPTOFTEN_VIEW

   - COM_ICD10CMMMP_VIEW

   - COM_ICD10PCS_VIEW

   - COM_ICD10PCS_DEPTOFTEN_VIEW

   - COM_ICD10_PCSMMP_VIEW

   - COM_ICD10_PSC_LEVEL_VIEW

   ![image-20210810181800069](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210810181800069.png)

   

2. 藥囑

   - ComMedTypeView

     ↑ 應該是從COM_MED_TYPE_MST和COM_MED_TYPE_DTL組的

   - ComMedBasicView

   - ComMedMappingDiagView

   - ComMedamtView

   - ComMedAttributeView

   - ComMedCommentView

   - ComMedReplaceView

   - ComMedAllergyRecView

   - ComMedThinnerView

   - ComMedThinnerAdditionView

3. 處置

4. 檢驗檢查

5. 手術麻醉

6. 衛材

7. ICD9

8. 計價(?)

...



## 診所版已經有用到的

- 病患

  /api/clin/com/ComChrbas

- ICD10CM國際標準碼主檔

  /api/clin/com/ComIcd10cm

- ICD10章節維護

  /api/clin/com/ComIcd10Chapter/getICD10CMOrderTreeNode

