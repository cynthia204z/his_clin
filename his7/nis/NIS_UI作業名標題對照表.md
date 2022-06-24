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
      width: 140px;
      display: inline-block;
      text-align: -webkit-right;
    }
    .nis {
      color: chocolate;
    }
    .nis.title{
      background: chocolate;
    }
    .title {
      padding: 5px;
      font-weight: 800;
      color: #fff;
    }
    .thin{
     	width: calc(52% - 150px);
      font-weight: 300;
      mix-blend-mode: color-dodge;
      margin-left: 110px;
      text-align: left;
    }
    .thin.c-2nd{
      mix-blend-mode: color-burn;
      margin-left: 140px;
    }
    .thin.c-3rd{
      mix-blend-mode: luminosity;
      margin-left: 170px;
    }
    .row{
      vertical-align: middle;
      transition: all 0.1s linear;
    }
    .row:hover{
      position: relative;
      background: #433535;
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
    .util-pkg{
      color: #009926;
    }
  </style>
  <br>
  <br>
  <div id="NIS"></div>
  <h2 class="nis">NIS護囑</h2>
  <div class="title nis">consult</div><br>
  <div class="row"><div class="codeName nis">nis7020</div> 照會作業 </div>
  <div class="row"><div class="codeName nis">nis7020S</div> 照會回覆 </div>
  <br>
  <div class="title nis">discharge</div><br>
  <div class="row"><div class="codeName nis">nis9020</div> 出院護理 </div>
  <br>
  <div class="title nis">handOver</div><br>
  <div class="row"><div class="codeName nis">nis8020</div> 交班(X) </div></div>
<div class="row"><div class="codeName nis">nis8030</div> 交班作業=>交班 </div>
<div class="row"><div class="codeName nis thin">⌊___ nisEventHandOverPage</div> 交辦事項 </div>
<div class="row"><div class="codeName nis thin c-2nd">⌊___ NisHandOverNewForm</div> 交辦事項 </div>
<div class="row"><div class="codeName nis thin c-2nd c-3rd">⌊___ handOverEvent</div> 醫囑交辦事項 </div>
<div class="row"><div class="codeName nis thin c-2nd c-3rd">⌊___ recordShift</div> 當班處置事項 </div>
<div class="row"><div class="codeName nis thin c-2nd c-3rd">⌊___ record</div> 新增交辦事項 </div>
<div class="row"><div class="codeName nis thin c-2nd">⌊___ NisNonconfirmHandOverForm</div> 未執行事項 </div>
<div class="row"><div class="codeName nis thin c-2nd c-3rd">⌊___ medTable</div> 藥囑 </div>
<div class="row"><div class="codeName nis thin c-2nd c-3rd">⌊___ orderTable</div> 醫囑 </div>
<div class="row"><div class="codeName nis thin c-2nd c-3rd">⌊___ recordTable</div> 紀錄 </div>
<div class="row"><div class="codeName nis thin c-2nd c-3rd">⌊___ signTable</div> 簽章 </div>
<div class="row"><div class="codeName nis thin c-2nd c-3rd">⌊___ chemoTable</div> 化療藥物出庫簽核 </div>
<div class="row"><div class="codeName nis thin c-2nd">⌊___ NisChgEventHandOverForm</div> 異動摘要 </div>
<div class="row"><div class="codeName nis thin">⌊___ nisOrder</div> 醫囑 </div>
<div class="row"><div class="codeName nis thin">⌊___ nisMed</div> 藥囑 </div>
<div class="row"><div class="codeName nis thin">⌊___ nisConsult</div> 會診 </div>
<div class="row"><div class="codeName nis thin">⌊___ nisOr</div> 手術 </div>
<div class="row"><div class="codeName nis thin">⌊___ nisDiet</div> 飲食 </div>
<div class="row"><div class="codeName nis thin">⌊___ nisBlod</div> 輸血 </div>
<div class="row"><div class="codeName nis thin">⌊___ nisHealthProblem</div> 健康問題 </div>
<div class="row"><div class="codeName nis thin">⌊___ nisHandoverPlatform</div> 團隊交班平台 </div>
<div class="row"><div class="codeName nis thin util-pkg">⌊___ dialog</div>  </div>
<div class="row"><div class="codeName nis thin c-2nd">⌊___ NisHandOverDtlRemedyDialog</div> 帶回上一班事項 </div>
<div class="row"><div class="codeName nis thin c-2nd">⌊___ PublishMsgDialog</div> 重要訊息清單 </div>
<div class="row"><div class="codeName nis thin c-2nd">⌊___ NisHandOverQueryDialog</div> (交班/交辦事項/查詢按鈕) </div>
<div class="row"><div class="codeName nis">nis8040Table</div> 跨單位交班查詢 </div>
<div class="row"><div class="codeName nis">nis8050</div> 簽收 </div>

  <br>
  <div class="title nis">ordercomfirm</div><br>
<div class="row"><div class="codeName nis">nis3021S</div> </div>  
<div class="row">  <div class="codeName nis">nis3023</div> 醫囑確認 </div>  
<div class="row">  <div class="codeName nis">nis3031</div> 藥囑確認 </div>  
<div class="row">  <div class="codeName nis">nis3040</div> 退藥作業 </div>  
<div class="row">  <div class="codeName nis">nis3040S</div> 護理站退藥 </div>  
<div class="row">  <div class="codeName nis">nis3060</div> 化療確認 </div>  
<div class="row">  <div class="codeName nis">nis3070</div> 醫囑清單 </div>  
<div class="row">  <div class="codeName nis">nis3080</div> 耗材使用查詢 </div>  
<div class="row">  <div class="codeName nis">nis3090</div> 看護申請 </div>  
<div class="row">  <div class="codeName nis">nis3110</div> 帳務查詢 </div>  
<div class="row">  <div class="codeName nis">nis3111</div> 緊急醫令 </div>  

  <br>
  <div class="title nis">outservice</div><br>
<div class="row"><div class="codeName nis">nisa020</div> 出院準備 </div>
<div class="row">  <div class="codeName nis">nisa030</div> 出院電訪 </div>  

  <br>
  <div class="title nis">plan</div><br>
<div class="row">  <div class="codeName nis">nis5020</div> 計畫 </div>  

  <br>
  <div class="title nis">teaching</div><br>
<div class="row"> <div class="codeName nis">nisB020</div> 衛教作業 </div>  

  <br>
  <div class="title nis">utility</div><br>
<div class="row"><div class="codeName nis">nis1010</div> 護理系統代碼設定 </div>  
<div class="row">  <div class="codeName nis">nis1020</div> 常用項維護 </div>  
<div class="row">  <div class="codeName nis">nis1050</div> 代簽護理人員設定 </div>  
<div class="row">  <div class="codeName nis">nis1051</div> 實習護理人員設定 </div>  
<div class="row">  <div class="codeName nis">nis1060</div> 補簽 </div>  
<div class="row">  <div class="codeName nis">nis1070</div> 片語維護 </div>  
<div class="row">  <div class="codeName nis">nis3022</div> 耗材設定 </div>  
<div class="row">  <div class="codeName nis">nis3025</div> 耗材常用項維護 </div>  
<div class="row">  <div class="codeName nis">nis3027</div> 藥品耗材常用項維護 </div>  
<div class="row">  <div class="codeName nis">nis3100</div> 輸送查詢 </div>  
<div class="row">  <div class="codeName nis">nis3111</div> 緊急醫囑片語維護 </div>  
<div class="row">  <div class="codeName nis">nis3120</div> 化療退藥 </div>  
<div class="row">  <div class="codeName nis">nis7010</div> 照會維護 </div>  
<div class="row">  <div class="codeName nis">nis8040Tree</div> 跨單位交班 </div>  
<div class="row">  <div class="codeName nis">nisB010</div> 衛教維護 </div>  
<div class="row">  <div class="codeName nis">nisB011</div> 衛教問卷 </div>  
<div class="row"><div class="codeName nis">nisC020</div>  </div>  
<div class="row">  <div class="codeName nis">nisTipMaintain</div> 提示維護 </div>  
<div class="row">  <div class="codeName nis">nisOerEpdHis</div> 急診病患動向 </div>  

  <br>
</div>