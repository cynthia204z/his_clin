<div style="font-family: monospace">
  <style type="text/css" scoped>
    body{
      background: #333;
      color: #eee;
    }
    h2{
      font-weight: 900;
      font-size: 72px;
      margin: 50px 0 10px 0 ;
      font-family: sans-serif;
      padding-bottom: 8px;
      margin: 50px 0 10px 0;
      border-bottom: none;
      padding-left: 35px;
    }
    .codeName {
      font-weight: bold;
      padding: 2.5px 15px 2.5px 0;
      width: 200px;
      display: inline-block;
      text-align: -webkit-right;
    }
    .comm {
      color: darkseagreen;
    }
    .comm.title{
      background: darkseagreen;
    }
    .cpoe {
      color: goldenrod;
    }
    .cpoe.title{
      background: goldenrod;
    }
    .ierpat {
      color: cornflowerblue;
    }
    .ierpat.title{
      background: cornflowerblue;
    }
    .oerpat {
      color: lightcoral;
    }
    .oerpat.title{
      background: lightcoral;
    }
    .title {
      padding: 5px;
      font-weight: 800;
      color: #fff;
    }
    .thin{
      width: calc(50% - 150px);
		  margin-left: 150px;
      text-align: left;
      font-weight: 300;
      mix-blend-mode: difference;
    }
    .row{
      vertical-align: middle;
      transition: all 0.1s linear;
    }
    .row:hover{
      position: relative;
      background: #272727;
    }
    .row:hover::before{
      content: "▶";
      transition: all 0.1s linear;
      padding: 2.5px 0;
      color: gray;
      font-weight: bold;
      position: absolute;
      left: 10px;
    }
  </style>
  <br>
  <br>
  <div id="COMM"></div>
  <h2 class="comm">COMM醫囑共用</h2>
  <div class="title comm">dialog</div><br>
  <div class="row"><div class="codeName comm">allergyRecordDialog</div> 過敏記錄 </div>
  <br>
  <div class="title comm">page</div><br>
  <div class="row"><div class="codeName comm">Comm1010Page</div> 代碼主檔 </div>
  <div class="row"><div class="codeName comm">Comm1020Page</div> 衛教檔案設定 </div>
  <div class="row"><div class="codeName comm">Comm1030Page</div> 醫療目標點數 </div>
  <div class="row"><div class="codeName comm">Comm2010RegisterPage</div> 門診預約掛號 </div>
  <div class="row"><div class="codeName comm">Comm3010Page</div> 重要病史 </div>
  <div class="row"><div class="codeName comm">Comm5050newPage</div> 化療處方 </div>
  <div class="row"><div class="codeName comm thin">⌊___ Comm5050_ApyLog</div> 事前審查紀錄 </div>
  <div class="row"><div class="codeName comm thin">⌊___ Comm5050_History</div> 歷史療程 </div>
  <div class="row"><div class="codeName comm thin">⌊___ Comm5050_Order</div> 化療表單 </div>
  <div class="row"><div class="codeName comm thin">⌊___ Comm5050_OrderTW</div> 化療處方明細 </div>
  <div class="row"><div class="codeName comm thin">⌊___ Comm5050_TypeSelectionTW</div> 選擇化療處方明細種類 </div>
	<div class="row"><div class="codeName comm">Comm5060Page</div> 診斷書 </div>
  <div class="row"><div class="codeName comm thin">⌊___ comm5060_CBorn</div> 中文出生證明書 </div>
  <div class="row"><div class="codeName comm thin">⌊___ comm5060_Death</div> 死亡證明書 </div>
  <div class="row"><div class="codeName comm thin">⌊___ comm5060_EBorn</div> 英文出生證明書 </div>
  <div class="row"><div class="codeName comm thin">⌊___ comm5060_EDeath</div> 英文死亡證明書 </div>
  <div class="row"><div class="codeName comm thin">⌊___ comm5060_English</div> 英文診斷書 </div>
  <div class="row"><div class="codeName comm thin">⌊___ comm5060_General</div> 一般診斷書 </div>
  <div class="row"><div class="codeName comm">Comm5080Page</div> 預約入院作業 </div>
  <div class="row"><div class="codeName comm">Comm5090Page</div> 會診醫師排班 </div>
  <div class="row"><div class="codeName comm thin">⌊___ Comm5090_TW</div> 複製月排班表 </div>
  <div class="row"><div class="codeName comm">Comm6040Page</div> 會診單填寫 </div>
  <div class="row"><div class="codeName comm">Comm6041Page</div> 會診單回覆 </div>
  <br>
  <div class="title comm">view</div><br>
  <div class="row"><div class="codeName comm">EmrChemoPackage</div> 化療套餐 </div>  
  <br>
  <br>
  <div id="CPOE"></div>
  <h2 class="cpoe">CPOE全院項</h2>
  <div class="title cpoe">dialog</div><br>
  <div class="codeName cpoe">InsCodeToPcsDialog</div> ICD10PCS Search Dialog <br>
  <div class="codeName cpoe">OrderCircleDialog</div> 可用頻次(用法) <br>
  <div class="codeName cpoe">PhmPathDialog</div> 可用途徑 <br>
  <div class="codeName cpoe">searchDialog</div> 醫令選項(最外層orderType) <br>
  <div class="codeName cpoe">searchOrderDialog</div> 醫令選項(最外層orderSys) <br>
  <br>
  <div class="title cpoe">view</div><br>
  <div class="codeName cpoe">CpoeFrequentPage</div> 常用項設定 <br>
  <div class="codeName cpoe thin">⌊___ deptEmrfrequent.vue</div> 科常用 <br>
  <div class="codeName cpoe thin">⌊___ docEmrfrequent.vue</div> 醫師常用 <br>
  <div class="codeName cpoe">CpoePkgPage</div> 套餐設定 <br>
  <div class="codeName cpoe thin">⌊___ deptEmrpkg.vue</div> 科套餐 <br>
  <div class="codeName cpoe thin">⌊___ docEmrpkg.vue</div> 醫師套餐 <br>
  <div class="codeName cpoe">CpoeFrerquentImagePage</div> 常用圖檔 <br>
  <div class="codeName cpoe thin">⌊___ deptimg.vue</div> 科圖檔 <br>
  <div class="codeName cpoe thin">⌊___ docimg.vue</div> 醫師圖檔 <br>
  <br>
  <br>
  <div id="IERPAT"></div>
  <h2 class="ierpat">IERPAT住院醫囑</h2>
  <div class="title ierpat">dialog</div><br>
  <div class="codeName ierpat">comm5080Dialog</div> 預約入院作業 <br>
  <div class="codeName ierpat">Ier1080_DittoDialog</div> 病患問題 Ditto Dialog <br>
  <div class="codeName ierpat">Ier1080_TitleDialog</div> 病患問題管理 <br>
  <div class="codeName ierpat">Ier2010_1Dialog</div> 自備藥 <br>
  <div class="codeName ierpat">Ier2010_ReprintDialog</div> 重印作業 <br>
  <div class="codeName ierpat">Ier2011_DrugKeepQtyDialog</div> 藥品剩餘量 <br>
  <div class="codeName ierpat">Ier2012_RePrintDialog</div> 預約住院處方  同意書 <br>
  <div class="codeName ierpat">Ier3020_TitleDialog</div> 選擇出院病摘 <br>
  <div class="codeName ierpat">Ier3050_DittoDialog</div> 醫師交班Ditto Dialog <br>
  <div class="codeName ierpat">printerLocation_1Dialog</div> 印表機選擇 <br>
  <br>
  <div class="title ierpat">page</div><br>
  <div class="codeName ierpat">EmrQueryTprInfo</div> TPR資訊 <br>
  <div class="codeName ierpat">Ier1080</div> 病患問題管理 <br>
  <div class="codeName ierpat">Ier2010</div> 一般處方 <br>
  <div class="codeName ierpat">Ier2011</div> 帶藥處方 <br>
  <div class="codeName ierpat">Ier2012</div> 預約住院處方 <br>
  <div class="codeName ierpat">Ier2013</div> 膳食處方 <br>
  <div class="codeName ierpat">Ier2014</div> 輸血處方 <br>
  <div class="codeName ierpat">Ier2020</div> 診斷維護 <br>
  <div class="codeName ierpat">Ier2040</div> 出院準備作業 <br>
  <div class="codeName ierpat">Ier2060</div> 以預約住院名單/入院病患管理 <br>
  <div class="codeName ierpat">Ier3020</div> 病歷首頁維護 <br>
  <div class="codeName ierpat">Ier3050</div> 醫師交班作業 <br>
  <br>
  <div class="title ierpat">view</div><br>
  <div class="codeName ierpat">EmrQueryWardRoundsPage</div> 醫師查詢病患清單(TPR) <br>
  <div class="codeName ierpat">IerDocAuthorizationPage</div> 主治醫師授權 <br>
  <div class="codeName ierpat">IerMainPage</div> 住院醫囑病患首頁 <br>
  <div class="codeName ierpat">PatitentListPage</div> 住院病患清單 <br>
  <br>
  <br>
  <div id="OERPAT"></div>
  <h2 class="oerpat">OERPAT門急診醫囑</h2>
  <div class="title oerpat">dialog</div><br>
  <div class="codeName oerpat">allergyRecordDialog</div> 過敏記錄 <br>
  <div class="codeName oerpat">capHcLogDialog</div> 檳菸史 <br>
  <div class="codeName oerpat">chronicDialog</div> 連續處方箋記錄 <br>
  <div class="codeName oerpat">comm3010PageDialog</div> 重要病史 <br>
  <div class="codeName oerpat">comm5050NewPageDialog</div> 化療處方 <br>
  <div class="codeName oerpat">comm5060PageDialog</div> 診斷書開立 <br>
  <div class="codeName oerpat">commConsultDialog</div> 會診 <br>
  <div class="codeName oerpat">copyDiagFreqDialog</div> 儲存診斷至常用項 <br>
  <div class="codeName oerpat">copySOPNoteDialog</div> 複製範本 (SOPNoteEditPage SOP範本) <br>
  <div class="codeName oerpat">copySOPPhraseDialog</div> 複製片語 (SOPPhraseEditPage 門急診片語) <br>
  <div class="codeName oerpat">DittoOtherDialog</div> Do其他 <br>
  <div class="codeName oerpat">EerICUFormDialog</div> ICU 交班表 (EpdHisDialog 病患動向) <br>
  <div class="codeName oerpat">EerPatAADDialog</div> 違背醫囑自動出院報告單 (EpdHisDialog 病患動向) <br>
  <div class="codeName oerpat">EerPatTeachDialog</div> 病患衛教 (EpdHisDialog 病患動向) <br>
  <div class="codeName oerpat">emrQueryMainPageDialog</div> 病患就診記錄 <br>
  <div class="codeName oerpat">emrRecordDialog</div> 病患就醫紀錄 <br>
  <div class="codeName oerpat">EpdHisDialog</div> 病患動向 <br>
  <div class="codeName oerpat">HospOutDialog</div> 請選擇 轉出院所 (EpdHisDialog 病患動向) <br>
  <div class="codeName oerpat">icCardDialog</div> 取健保IC卡序 <br>
  <div class="codeName oerpat">icd10AIDialog</div> 推薦診斷碼 <br>
  <div class="codeName oerpat">ier2012Dialog</div> 辦理住院 <br>
  <div class="codeName oerpat">ier2060Dialog</div> 已預約住院名單查詢 <br>
  <div class="codeName oerpat">IpdShiftHistoryDialog</div> 出院交班歷程 <br>
  <div class="codeName oerpat">LisResultDialog</div> 檢驗資料 <br>
  <div class="codeName oerpat">oerPatImageDialog</div> 門診病患圖檔 <br>
  <div class="codeName oerpat thin">⌊___ freqImgDialog</div> 從常用新增圖檔 <br>
  <div class="codeName oerpat">PhraseDialog</div> 常用片語 <br>
  <div class="codeName oerpat">regRegisterDialog</div> 門診預掛 <br>
  <div class="codeName oerpat">rePrintDialog</div> 重印報表 <br>
  <div class="codeName oerpat">SOPLoadDialog</div> 讀取SOP範本 <br>
  <div class="codeName oerpat">SOPSaveDialog</div> 儲存SOP範本 <br>
  <br>
  <div class="title oerpat">form</div><br>
  <div class="codeName oerpat">SOPform</div> SOP組件 <br>
  <br>
  <div class="title oerpat">page</div><br>
  <div class="codeName oerpat">emrlisresult</div> 檢驗報告 <br>
  <div class="codeName oerpat">emrpatconsult</div> 手術記錄/會診紀錄 <br>
  <div class="codeName oerpat">emrpatnote</div> 檢查報告 <br>
  <br>
  <div class="title oerpat">table</div><br>
  <div class="codeName oerpat">oerdrug</div> 藥囑Table組件 <br>
  <div class="codeName oerpat">oerorder</div> 醫囑Table組件 <br>
  <div class="codeName oerpat">oerpatdiag10dtl</div> 診斷Table組件 <br>
  <br>
  <div class="title oerpat">view</div><br>
  <div class="codeName oerpat">EerPatinsListDocPage</div> 急診病患清單(醫師) <br>
  <div class="codeName oerpat">EmrRecordPage</div> 歷次就醫紀錄 <br>
  <div class="codeName oerpat">ErCareCenterListPage</div> 急診照護查詢 <br>
  <div class="codeName oerpat thin">⌊___ EmrReportACS001Table</div> 急性冠心症 ACS <br>
  <div class="codeName oerpat thin">⌊___ EmrReportCVA001Table</div> 急性腦中風 CVA <br>
  <div class="codeName oerpat thin">⌊___ EmrReportTRAUMA001Table</div> 緊急外傷 TRAUMA <br>
  <div class="codeName oerpat thin">⌊___ EmrReportSepsis001Table</div> 敗血性休克/嚴重敗血症 <br>
  <div class="codeName oerpat">ErPatinsPage</div> 急診醫囑病患首頁 <br>
  <div class="codeName oerpat">OerMainPage</div> 門診醫囑病患首頁 <br>
  <div class="codeName oerpat">OerPatBasList</div> 門診病患清單 <br>
  <div class="codeName oerpat">OerRoomListPage</div> 門診診間清單 <br>
  <div class="codeName oerpat">SOPNoteEditPage</div> SOP範本 <br>
  <div class="codeName oerpat">SOPPhraseEditPage</div> 門急診片語 <br>
  <br>
  <br>
</div>











<div style="position: fixed; top: 10px; left: 0; padding:10px 20px 10px 0; border-radius: 0 15px 15px 0;
    justify-content: space-between;display: flex; flex-direction: column;">
  <style type="text/css" scoped>
    .item{
      width:100px;
      color: #fff;
      font-weight:800;
      padding:5px;
      text-decoration: none;
      border:2px solid transparent;
      text-align: center;
      transition-duration:.2s; 
    }
    .item:hover{
      text-decoration: none;
      border:2px solid #fff;
      width: 110px;
    }
    .comm-menu{
      background:darkseagreen;
    }
    .cpoe-menu{
      background:goldenrod;
    }
    .ierpat-menu{
      background:cornflowerblue;
    }
    .oerpat-menu{
      background:lightcoral;
    }
    .menu-title{
      width:100px;
      color: darkgray;
      font-weight:800;
      padding:5px;
      text-align: center;
      border:2px solid transparent;
    }
  </style>
  <div class="menu-title">EMR</div>
  <a class="item comm-menu" href="#COMM">COMM</a>
  <a class="item cpoe-menu" href="#CPOE">CPOE</a>
  <a class="item ierpat-menu" href="#IERPAT">IERPAT</a>
  <a class="item oerpat-menu" href="#OERPAT">OERPAT</a>
</div>






