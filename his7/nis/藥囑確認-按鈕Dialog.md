# 藥囑確認 按鈕Dialog

## One Touch 檢驗查詢

HIS7: nis3021S

UI位置: top toolbar>One Touch

Table: NIS_ONE_TOUCH_DATA

HIS3 Front End Source: Nis3021SgEditPage

Dictionary:

```xml
<YDataDictionaryObject objectId="nisOneTouchDataDTO" externalName="nisOneTouchDataDTO" className="com.hcsaastech.ehis.nis.webservice.orderconfirm::NisOneTouchDataDTO">
  <YDataDictionaryField fieldId="id" externalName="id" label="ID" dataType="Integer" isReadOnly="true" />
  <YDataDictionaryField fieldId="encounterNo" externalName="encounterNo" label="住院序號" dataType="String" isRequired="true" />
  <YDataDictionaryField fieldId="executeDateTime" externalName="executeDateTime" label="檢驗時間"    dataType="DateTime" metaDataType="DTime" />            
  <YDataDictionaryField fieldId="applyItemSeq" externalName="applyItemSeq" label="序號" dataType="String"  />
  <YDataDictionaryField fieldId="indicationCode" externalName="indicationCode" label="代碼" dataType="String"/>
  <YDataDictionaryField fieldId="content" externalName="content" label="血糖值(mg/dl)" dataType="String" />
  <YDataDictionaryField fieldId="ivpDate" externalName="ivpDate" label="施打日期時間"  dataType="DateTime" metaDataType="DTime" />
  <YDataDictionaryField fieldId="ivpMedCode" externalName="ivpMedCode" label="胰島素注射品項" dataType="String" dataProviderId="NisOneTouchMed"/>
  <YDataDictionaryField fieldId="ivpMedCodeName" externalName="ivpMedCodeName" label="胰島素注射" dataType="String"/>
  <YDataDictionaryField fieldId="ivpMedName" externalName="ivpMedName" label="胰島素注射備註" dataType="String" />
  <YDataDictionaryField fieldId="medQty" externalName="medQty" label="數量(unit)" dataType="String" />
  <YDataDictionaryField fieldId="displayName" externalName="displayName" label="醫囑名稱" dataType="String" />
  <YDataDictionaryField fieldId="testByName" externalName="testByName" label="執行者" dataType="String" />
  <YDataDictionaryField fieldId="ivpPosition" externalName="ivpPosition" label="施打部位" dataType="String" dataProviderId="NisOneTouchPosition" />
</YDataDictionaryObject>
```

GetQuery:

```type
queryId="NisOneTouchData nisOneTouchDataDTO"
```

<span style="color:orange;border:1px solid; padding: 2px 5px;">進度</span>

- [ ] UI
- [ ] DATA

## 給藥歷史

His7: NisMedHistoryPopUpWindow

UI位置: top toolbar>給藥歷史

Table: NIS_EXECUTE_MED_RECORD

HIS3 Front End Source: NisMedHistoryPopUpWindow

Dictionary: NisExecuteMedRecordDictionary

GetQuery:

```type
queryId="NisExecuteMedRecord nisExecuteMedRecordDTO"
```

<span style="color:orange;border:1px solid; padding: 2px 5px;">進度</span>

- [x] UI
- [ ] DATA

## 出院帶藥

His7: NisDischargeMedDialog

UI位置: top toolbar>出院帶藥

Table: NIS_IER_DRUG_VIEW、NIS_EXECUTE_MED_RECORD

HIS3 Front End Source: NisDischargeMedLov

ResultDTO: uiGetDischgMed

<span style="color:orange;border:1px solid; padding: 2px 5px;">進度</span>

- [x] UI
- [ ] DATA

## 條碼給藥

His7: NisMedPrepareConfirmDialog

UI位置: tab toolbar>條碼給藥

HIS3 Front End Source: NisMedPrepareConfirmLov

<span style="color:orange;border:1px solid; padding: 2px 5px;">進度</span>

- [x] UI
- [ ] DATA

## 給藥單列印

His7: NisDrugRecordPrintSelectDialog

UI位置: top toolbar>給藥單列印

HIS3 Front End Source: NisDrugRecordPrintSelectLov

<span style="color:orange;border:1px solid; padding: 2px 5px;">進度</span>

- [x] UI
- [ ] Action

## 管制藥列印

His7: NisControlDrugPrintDialog

UI位置: top toolbar>管制藥列印

HIS3 Front End Source: NisControlDrugPrintLov

<span style="color:orange;border:1px solid; padding: 2px 5px;">進度</span>

- [x] UI
- [ ] Action
