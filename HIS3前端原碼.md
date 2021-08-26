```xml
<hc:ZQuery id="query" serviceId="OerPatMgmtRoService" logicId="OerPatMgmtRoLogic" offset="0" maxRows="1"
    dtoId="OerPatbasDTO" queryId="OerPatbas oerPatbasDTO" queryFunction="uiGetOerPatbasXML">
   <hc:criteria>
      <hc:ZQueryCriterion operator="oerPatbasDTO.oeiType = 'O' and"/>
      <hc:ZQueryCriterion id="entNoCri" fieldKey="oerPatbasDTO.encounterNo" operator="=" value=""/>
      <!--hc:ZQueryCriterion operator="and oerPatbasDTO.status != '4' and oerPatbasDTO.status != '9' and oerPatbasDTO.deleteFlag != 'Y'"/-->
   </hc:criteria>
</hc:ZQuery>
```

- queryId：資料表 

- serviceId：程式間做為橋樑的程式

- ==重要==：queryFunction → 查詢的程式 →使用這個可以去後端找程式

- ZQueryCriterion：是 `where` 條件的意思，比如 `"oerPatbasDTO.oeiType = 'O' and....."`

  ![image-20210826102655925](https://raw.githubusercontent.com/LinYurou/PictureBed2/main/20210826102703.png)



```xml
<hc:ZQueryCriterion id="entNoCri" fieldKey="oerPatbasDTO.encounterNo" operator="=" value=""/>
```

查詢 "就醫序號" 後，會把這個 放入的條件 給一個 名稱 id="entNoCri" 

在該頁面的原碼 上搜尋此 名稱，可以追蹤到一個  `checkPatbas()` 方法

![image-20210826103021175](https://raw.githubusercontent.com/LinYurou/PictureBed2/main/20210826103021.png)











