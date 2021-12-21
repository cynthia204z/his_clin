## index.vue

```vue
<template>
  <div class="JNPF-common-layout-center" style="background: #fff; border: 1px solid #fff">
    <el-menu
      :default-active="activeIndex"
      class="el-menu-demo bg-color-3 selector"
      mode="horizontal"
      @select="menuSelect"
      style="display:flex"
    >
      <div v-for="(item, index) in menuOptions" :key="index">
        <el-submenu v-if="item.children" class="submenu" :index="item.name">
          <template slot="title">{{ item.title }}</template>
          <el-menu-item
            v-for="(subitem, index) in item.children"
            :key="index"
            :index="subitem.name"
          >{{ subitem.title }}</el-menu-item>
        </el-submenu>
        <el-menu-item v-if="!item.children" :index="item.name">{{ item.title }}</el-menu-item>
      </div>
    </el-menu>
    <div class="JNPF-common-layout" style="background: #fff; height: calc(100% - 30px)">
      <div
        class="JNPF-common-layout-left _panel"
        :class="{ 'leftpanel-change': !styleStatus.leftPanelIsShow }"
      >
        <el-form @submit.native.prevent>
          <groupTitle class="xs" content="病患資訊" />
          <el-form-item
            v-for="(item, index) in patinfoData"
            :key="index"
            :label="item.label"
            label-width="70px"
            class="_patinfo"
          >
            <span v-if="item.label != '病歷號'">{{ item.value }}</span>
            <el-button v-if="item.label === '病歷號'" type="text">
              {{
              item.value
              }}
            </el-button>
          </el-form-item>
          <el-form-item label="過敏" label-width="70px" class="_patinfo"></el-form-item>
          <el-form-item style="margin-left: 20px">
            <el-input true type="textarea" :autosize="{ minRows: 15, maxRows: 15 }"></el-input>
          </el-form-item>
        </el-form>
      </div>
      <div class="panelshowctrlbtn border-color-2">
        <el-button
          :title="styleStatus.leftPanelIsShow ? '收合' : '展開'"
          style="margin-right: 10px"
          @click="styleStatus.leftPanelIsShow = !styleStatus.leftPanelIsShow"
          type="text"
        >
          <i class="icon-ym icon-ym-nav-next" v-if="!styleStatus.leftPanelIsShow"></i>
          <i class="icon-ym icon-ym-nav-prev" v-if="styleStatus.leftPanelIsShow"></i>
        </el-button>
        <span v-if="!styleStatus.leftPanelIsShow" class="font-color-1">病患資訊 ·· {{ data.patName }}</span>
      </div>

      <div class="JNPF-common-layout-center tabsborder">
        <el-tabs
          v-model="editableTabsValue"
          type="border-card"
          class="JNPF-el_tabs _tabs"
          closable
          @tab-remove="removeTab"
          @tab-click="clickTab"
        >
          <el-tab-pane
            lazy
            class="JNPF-common-layout"
            style="width: 100%; background: #fff"
            v-for="(item, index) in editableTabs"
            :key="item.name"
            :index="index"
            :label="item.title"
            :name="item.name"
          >
            <!--            &lt;!&ndash; 彙總病歷資訊、查詢檢驗報告、查詢檢查報告、查詢病歷類別 &ndash;&gt;-->
            <EmrQueryMain
              v-if="item.name.indexOf('EmrQueryMain') != -1"
              :fromExtraSystemPatientData="data"
              :fromExtraSystem="true"
              :activePanel="EmrQueryMainActivePanel"
            ></EmrQueryMain>
            <component
              v-else
              :is="item.name"
              :patData="data"
              :patInfo="data"
              :docInfo="docInfo"
              :childDialogModal="true"
              @openIer2011="menuSelect('Ier2011')"
              @openIer2012="menuSelect('Ier2012')"
              @openComm2010="menuSelect('Comm2010')"
              @openAllergyRecord="menuSelect('Comm3020')"
              @openComm5060="menuSelect('Comm5060')"
              @openComm6010="menuSelect('Comm6010')"
            ></component>
            <!-- TPR資訊 -->
            <!--            <EmrQueryTprInfo v-if="item.name === 'EmrQueryTprInfo'"></EmrQueryTprInfo>-->
            <!--            &lt;!&ndash; 病患就醫紀錄 &ndash;&gt;-->
            <!--            <EmrRecord v-if="item.name === 'EmrRecord'" :patData="data"></EmrRecord>-->
            <!--            &lt;!&ndash; 過敏 &ndash;&gt;-->
            <!--            <Comm3020 v-if="item.name === 'Comm3020'" :patData="data"></Comm3020>-->
            <!--            &lt;!&ndash; 一般處方 &ndash;&gt;-->
            <!--            <Ier2010 v-if="item.name === 'Ier2010'" :patInfo="data" :docInfo="docInfo" @openAllergyRecord="menuSelect('Comm3020')"></Ier2010>-->
            <!--            &lt;!&ndash; 診斷維護 &ndash;&gt;-->
            <!--            <Ier2020 v-if="item.name === 'Ier2020'" :patInfo="data" :docInfo="docInfo"></Ier2020>-->
            <!--            &lt;!&ndash; 化療處方 &ndash;&gt;-->
            <!--            <Comm5050 v-if="item.name === 'Comm5050'" :patInfo="data"></Comm5050>-->
            <!--            &lt;!&ndash; 帶藥處方 &ndash;&gt;-->
            <!--            <Ier2011 v-if="item.name === 'Ier2011'" :patInfo="data" :docInfo="docInfo"></Ier2011>-->
            <!--            &lt;!&ndash; 預約住院處方 &ndash;&gt;-->
            <!--            <Ier2012 v-if="item.name === 'Ier2012'" :patInfo="data" :docInfo="docInfo"></Ier2012>-->
            <!--            &lt;!&ndash; 膳食處方 &ndash;&gt;-->
            <!--            <Ier2013 v-if="item.name === 'Ier2013'"></Ier2013>-->
            <!--            &lt;!&ndash; 輸血處方 &ndash;&gt;-->
            <!--            <Ier2014  v-if="item.name === 'Ier2014'"></Ier2014>-->
            <!--            &lt;!&ndash; 病患問題管理 &ndash;&gt;-->
            <!--            <Ier1080 v-if="item.name === 'Ier1080'" :docInfo="docInfo"></Ier1080>-->
            <!--            &lt;!&ndash; 會診單填寫 &ndash;&gt;-->
            <!--            <Comm6040Ier v-if="item.name === 'Comm6040Ier'" :patInfo="data" :docInfo="docInfo"></Comm6040Ier>-->
            <!--            &lt;!&ndash; 會診單回覆 &ndash;&gt;-->
            <!--            <Comm6041Ier v-if="item.name === 'Comm6041Ier'" @openComm6010="menuSelect('Comm6010')"></Comm6041Ier>-->
            <!--            &lt;!&ndash; 開立診斷書 &ndash;&gt;-->
            <!--            <Comm5060 v-if="item.name === 'Comm5060'"></Comm5060>-->
            <!--            &lt;!&ndash; 出院準備作業 &ndash;&gt;-->
            <!--            <Ier2040 -->
            <!--              v-if="item.name === 'Ier2040'" -->
            <!--              @openComm2010="menuSelect('Comm2010')"-->
            <!--              @openIer2011="menuSelect('Ier2011')"-->
            <!--              @openComm5060="menuSelect('Comm5060')"-->
            <!--              @openIer2012="menuSelect('Ier2012')"></Ier2040>-->

            <!--            &lt;!&ndash; 病歷首頁維護 &ndash;&gt;-->
            <!--            <Ier3020  v-if="item.name === 'Ier3020'"></Ier3020>-->
            <!--            &lt;!&ndash; 醫師交班作業 &ndash;&gt;-->
            <!--            <Ier3050 v-if="item.name === 'Ier3050'" :patInfo="data" :docInfo="docInfo"></Ier3050>-->
            <!--            &lt;!&ndash; 重要病史 &ndash;&gt;-->
            <!--            <Comm3010 v-if="item.name === 'Comm3010'" :patInfo="data" @openAllergyRecord="menuSelect('Comm3020')"></Comm3010>-->
            <!--            &lt;!&ndash; 預約掛號/退掛號 &ndash;&gt;-->
            <!--            <Comm2010 v-if="item.name === 'Comm2010'" :patInfo="data"></Comm2010>-->
            <!--            &lt;!&ndash;手術紀錄單&ndash;&gt;-->
            <!--            <Or9010 v-if="item.name === 'Or9010'"></Or9010>-->
          </el-tab-pane>
        </el-tabs>
      </div>
    </div>
  </div>
</template>

<script>
import index from "./js/index.js";
export default index;
</script>

<style lang="scss" scoped>
.center-content {
  height: 50%;
  overflow: auto;
  &._top {
    border-bottom: 1px solid;
  }
}

._panel {
  margin-right: 0;
}
.tab1-lefttable {
  width: 250px;
  padding-right: 0;
  padding-bottom: 10px;
  margin-right: 0;
}
.leftpanel-change {
  width: 0px;
  overflow: hidden;
}
.panelshowctrlbtn {
  border-width: 0 1px 0 0;
  border-style: solid;
  width: 20px;
  text-align: center;
  span {
    font-size: 12px;
    width: 100%;
    -webkit-writing-mode: vertical-lr;
    writing-mode: vertical-lr;
  }
}
// .hideSidebar .submenu >>> .el-submenu > .el-submenu__title {
//   padding: 0 20px !important;
// }
.submenu {
  height: 30px;
  line-height: 30px;
  >>> .el-submenu__title {
    height: 30px !important;
    line-height: 30px !important;
  }
}
.hideSidebar .submenu {
  padding: 0 20px;
}
.selector {
  height: 30px;
  line-height: 30px;

  >>> .el-menu-item {
    height: 30px !important;
    line-height: 30px !important;
    padding: 0 20px !important;
    // transition: none;
    &.is-active {
      color: #fff !important;
    }
    &:not(.is-disabled):focus,
    .el-menu--horizontal .el-menu-item:not(.is-disabled):hover {
      color: #fff !important;
    }
  }
}
.tabsborder {
  border-top: 1px solid #fff;
}
._patinfo {
  margin: 0;
}

._tabs {
  >>> .el-tabs__header {
    margin: 0;
  }
}
.el-menu-demo >>> .el-submenu__icon-arrow {
  display: none !important;
}
.el-menu-demo >>> .el-submenu__icon-arrow:before {
  content: "";
}
</style>

```

## index.js

```js
import {menuOptions, otherMenu} from "@/views/his7/emr/ierpat/view/IerMainPage/js/static.js"
import EmrQueryTprInfo from "@/views/his7/emr/ierpat/page/EmrQueryTprInfo"
import EmrQueryMain from "@/views/his7/emrquery/emrquerymainpage"
import Comm3020 from "@/views/his7/emrquery/emrquery1090"
import EmrRecord from "@/views/his7/emr/oerpat/view/EmrRecordPage"
import Ier2010 from "@/views/his7/emr/ierpat/page/Ier2010"
import Ier2020 from "@/views/his7/emr/ierpat/page/Ier2020"
import Comm5050 from "@/views/his7/emr/comm/Comm5050newPage"
import Ier2011 from "@/views/his7/emr/ierpat/page/Ier2011"
import Ier2012 from "@/views/his7/emr/ierpat/page/Ier2012"
import Ier2013 from "@/views/his7/emr/ierpat/page/Ier2013"
import Ier2014 from "@/views/his7/emr/ierpat/page/Ier2014"
import Ier1080 from "@/views/his7/emr/ierpat/page/Ier1080"
import Comm6040Ier from "@/views/his7/emr/comm/Comm6040Page"
import Comm6041Ier from "@/views/his7/emr/comm/Comm6041Page"
import Comm5060 from "@/views/his7/emr/comm/Comm5060Page"
import Ier2040 from "@/views/his7/emr/ierpat/page/Ier2040"
import Ier3020 from "@/views/his7/emr/ierpat/page/Ier3020"
import Ier3050 from "@/views/his7/emr/ierpat/page/Ier3050"
import Comm3010 from "@/views/his7/emr/comm/Comm3010Page"
import Comm2010 from "@/views/his7/emr/comm/Comm2010RegisterPage"
import Or9010 from "@/views/his7/or/flow/oropnote"

export default {
  components: {
    EmrQueryTprInfo, //TPR資訊
    EmrQueryMain, //彙總病歷資訊、查詢檢驗報告、查詢檢查報告、查詢病歷類別
    EmrRecord, //病患就醫紀錄
    Comm3020, //過敏
    Ier2010, //一般處方
    Ier2020, //診斷維護
    Comm5050, //化療處方
    Ier2011, //帶藥處方
    Ier2012, //預約住院處方
    Ier2013, //膳食處方
    Ier2014, //輸血處方
    Ier1080, //病患問題管理
    Comm6040Ier, //會診單填寫
    Comm6041Ier, //會診單回覆
    Comm5060, //開立診斷書
    Ier2040, //出院準備作業
    Ier3020, //病歷首頁維護
    Ier3050, //醫師交班作業
    Comm3010, //重要病史
    Comm2010, //預約掛號/退掛號
    Or9010, //手術紀錄單
  },
  data() {
    return {
      docInfo: {
        title: "醫生名", // 開發期間暫用
        docCode: "test30000", // 開發期間暫用
        deptCode: "deptTest30000", // 開發期間暫用
        usageOei: "I", // 住院
      },
      data: this.$route.query.data, //patInfo
      patinfoData: [],
      patinfoLabel: [
        "住院序號",
        "病歷號",
        "姓名",
        "年齡",
        "生日",
        "床位",
        "科別",
        "主治醫師",
        "入院日期",
        "性別",
        "護理站",
      ],
      activeIndex: "",
      menuCurrentIndex: "",
      editableTabsValue: "EmrQueryTprInfo",
      editableTabsOptions: [],
      // 預設開啟的標籤頁
      editableTabs: [
        {
          title: "一般處方",
          name: "Ier2010",
        },
        {
          title: "病患個人資訊",
          name: "Summary",
        },
        {
          title: "TPR資訊",
          name: "EmrQueryTprInfo",
        },
      ],
      menuOptions: menuOptions,
      otherMenu: otherMenu,
      
      styleStatus: {
        leftPanelIsShow: true,
      },

      EmrQueryMainActivePanel: undefined,
    };
  },
  created() {
    this.initPatinfo();
    this.setEditableTabsOptions();
  },
  mounted () {
    this.$route.meta.zhTitle = `住院醫囑(${this.data.patName}  ${this.data.bedNo})`
    document.title = `住院醫囑(${this.data.patName}  ${this.data.bedNo}) - iAlice雲醫療平臺`
  },
  methods: {
    // 設定可以開啟的標籤頁
    setEditableTabsOptions() {
      this.menuOptions.forEach(t => {
        if (t.children) {
          t.children.forEach(c => {
            if (c.isPage) {
              this.editableTabsOptions.push(c)
            }
          })
        }
      })
      this.otherMenu.forEach(t => {
        this.editableTabsOptions.push(t)
      })
    },
    // 取得病患資料
    initPatinfo() {
      let data = this.data;
      let valueList = [
        data.encounterNo,
        data.chartNo,
        data.patName,
        data.age,
        data.birthDate,
        data.bedNo,
        data.deptName,
        data.vsName,
        data.admitDate,
        data.sexType,
        data.branchCode,
      ];
      for (let i = 0; i < valueList.length; i++) {
        let item = {
          label: this.patinfoLabel[i],
          value: valueList[i],
        };
        this.patinfoData.push(item);
      }
    },

    // 點選菜單
    menuSelect(index, path) {
      this.menuCurrentIndex = index;
      let selectItem = this.editableTabs.find((t) => t.name === index);
      if (selectItem) {
        if (selectItem.name.indexOf('EmrQueryMain') != -1) {
          this.EmrQueryMainActivePanel = this.editableTabsOptions.find((t) => t.name === index).activePanel
        }
        this.editableTabsValue = selectItem.name;
      } else {
        let newtab = this.editableTabsOptions.find((t) => t.name === index);
        if(newtab){
          if (newtab.name.indexOf('EmrQueryMain') != -1) {
            this.EmrQueryMainActivePanel = newtab.activePanel
          }
          this.addTab(newtab);
        }
      }
    },

    // 新增標籤頁
    addTab(targetName) {
      this.editableTabs.push({
        title: targetName.title,
        name: targetName.name,
      });
      this.editableTabsValue = targetName.name;
    },

    // 關閉標籤頁
    removeTab(targetName) {
      let tabs = this.editableTabs;
      let activeName = this.editableTabsValue;
      if (activeName === targetName) {
        tabs.forEach((tab, index) => {
          if (tab.name === targetName) {
            let nextTab = tabs[index + 1] || tabs[index - 1];
            if (nextTab) {
              activeName = nextTab.name;
            }
          }
        });
      }

      this.editableTabsValue = activeName;
      this.editableTabs = tabs.filter((tab) => tab.name !== targetName);
    },

    // 切換標籤頁
    clickTab(target) {
      if(target.name.indexOf('EmrQueryMain') != -1) {
        this.EmrQueryMainActivePanel = this.editableTabsOptions.find((t) => t.name === target.name).activePanel
      }
    }
  },
};

```

## static.js

```js
const menuOptions = [{
  title: "臨床資訊",
  name: "1",
  children: [{
      title: "TPR資訊",
      name: "EmrQueryTprInfo",
      isPage: true
    },
    {
      title: "彙總病歷資訊",
      name: "EmrQueryMain",
      activePanel: "emrquery1010",
      isPage: true
    },
    {
      title: "病患就醫紀錄",
      name: "EmrRecord",
      isPage: true
    },
    {
      title: "病患個人資訊",
      name: "Summary",
      isPage: true
    },
    {
      title: "健保卡資訊",
      name: "Icc2030",
      isPage: true
    },
    {
      title: "查詢檢驗報告",
      name: "EmrQueryMainLAB",
      activePanel: "emrquery1070",
      isPage: true
    },
    {
      title: "查詢檢查報告",
      name: "EmrQueryMainORDER",
      activePanel: undefined,
      isPage: true
    },
    {
      title: "查詢病歷類別",
      name: "EmrQueryMainMEDICAL_RECORD",
      activePanel: "emrquery1040",
      isPage: true
    },
    {
      title: "病患過敏記錄",
      name: "Comm3020",
      isPage: true
    },
    {
      title: "團隊照會明細",
      name: "Comm6012",
      isPage: true
    },
  ],
},
{
  title: "處方輸入",
  name: "2",
  children: [{
      title: "一般處方",
      name: "Ier2010",
      isPage: true
    },
    {
      title: "診斷維護",
      name: "Ier2020",
      isPage: true
    },
    {
      title: "化療處方",
      name: "Comm5050",
      isPage: true
    },
    {
      title: "帶藥處方",
      name: "Ier2011",
      isPage: true
    },
    {
      title: "預約住院處方",
      name: "Ier2012",
      isPage: true
    },
    {
      title: "膳食處方",
      name: "Ier2013",
      isPage: true
    },
    {
      title: "輸血處方",
      name: "Ier2014",
      isPage: true
    },
    {
      title: "居家醫囑單開立",
      name: "HomeCareOrder"
    },
    {
      title: "戒菸照會",
      name: "Nis7020"
    },
  ],
},
{
  title: "病歷作業",
  name: "3",
  children: [{
      title: "病歷撰寫",
      name: "DocNoteWeb"
    },
    {
      title: "病患問題管理",
      name: "Ier1080",
      isPage: true
    },
    {
      title: "會診單填寫",
      name: "Comm6040Ier",
      isPage: true
    },
    {
      title: "會診單回覆",
      name: "Comm6041Ier",
      isPage: true
    },
    {
      title: "多團隊交班平台(測試)",
      name: "CARE1020"
    },
    {
      title: "多團隊照會單(測試)",
      name: "CARE1030"
    },
    {
      title: "診斷書開立作業",
      name: "Comm5060",
      isPage: true
    },
    {
      title: "出院準備作業",
      name: "Ier2040",
      isPage: true
    },
    {
      title: "病歷首頁維護",
      name: "Ier3020",
      isPage: true
    },
    {
      title: "醫師交班作業",
      name: "Ier3050",
      isPage: true
    },
    {
      title: "重要病史登錄",
      name: "Comm3010",
      isPage: true
    },
    {
      title: "產科史登錄",
      name: "Comm3710"
    },
    {
      title: "手術記錄單",
      name: "Or9010",
      isPage: true
    },
    {
      title: "預立醫療流程",
      name: "PreOrderForm"
    },
    {
      title: "啟動跨團隊會議",
      name: "interDept"
    },
  ],
},
{
  title: "病歷表單",
  name: "4",
  children: [{
      title: "營養風險評分",
      name: "Ier3010"
    },
    {
      title: "加護病房營養評估表單",
      name: "DietIcuDataView"
    },
    {
      title: "外傷嚴重度評估",
      name: "Ier3030"
    },
    {
      title: "BSRS-5簡式健康量表",
      name: "ObsOpen"
    },
    {
      title: "國際前列腺症狀評分(I-PSS)問卷",
      name: "MRSR7940627"
    },
    {
      title: "兒科加護病房表單",
      name: "ICU40Form"
    },
    {
      title: "加護病房表單",
      name: "ICUForm"
    },
    {
      title: "產科病歷表NSD",
      name: "MRS709"
    },
    {
      title: "心導管檢查申請表",
      name: "MRAI077"
    },
    {
      title: "復健治療目標設定與治療計畫擬定(TEST)",
      name: "RehTreatGoalAndPlan",
    },
    {
      title: "X光骨盆計測表",
      name: "XRayPelvimetry"
    },
    {
      title: "自殺風險評估表",
      name: "GmsSuicideMedicalForm"
    },
    {
      title: "自殺危機評估表",
      name: "GmsSuicide2MedicalForm"
    },
    {
      title: "NIH Stroke Scale 檢查表",
      name: "NIHStrokeScale"
    },
    {
      title: "The Modified Rankin Scale (mRS) 評估表",
      name: "ConsultCVAD4",
    },
    {
      title: "急性缺血性腦中風之血栓溶解治療檢查表",
      name: "StrokertPA",
    },
    {
      title: "呼吸器患者整合性照護系統(IDS)延長加護病房照護記錄單",
      name: "MRS3073",
    },
    {
      title: "心衰竭治療照護表單",
      name: "HFTreatCare"
    },
    {
      title: "Hunt and Hess Scale嚴重度評估表",
      name: "ConsultCVAD1"
    },
    {
      title: "ICH嚴重度評估表",
      name: "ConsultCVAD2"
    },
    {
      title: "急性中風病人吞嚥功能篩檢表",
      name: "ConsultCVAD3"
    },
  ],
},
{
  title: "其它作業",
  name: "5",
  children: [{
      title: "事前審查申請",
      name: "Apy2040"
    },
    {
      title: "事前審查查詢",
      name: "Apy3050"
    },
    {
      title: "重大傷病申請",
      name: "Gms4050"
    },
    {
      title: "重大傷病查詢",
      name: "Gms4010"
    },
    {
      title: "重大傷病管理",
      name: "Ier1090"
    },
    {
      title: "愛滋紙卡輸入",
      name: "Gms8260"
    },
    {
      title: "ADR通報",
      name: "Phm5020"
    },
    {
      title: "ADR通報查詢",
      name: "Phm5010"
    },
    {
      title: "預約掛號/退掛號",
      name: "Comm2010",
      isPage: true
    },
    {
      title: "轉換主治醫師",
      name: "Adt2080"
    },
    {
      title: "傳染病通報",
      name: "Phn3020"
    },
    {
      title: "臨床路徑稽核報表",
      name: "IPD_CHECK_DRG_REPORT"
    },
    {
      title: "癌症病情告知",
      name: "capTruthTelling"
    },
    {
      title: "癌症治療計畫書",
      name: "cap80A0"
    },
    {
      title: "資源共享回覆單",
      name: "XRAYP5060"
    },
    {
      title: "老人整合計畫",
      name: "Nis7030"
    },
    {
      title: "心衰竭收案",
      name: "HFDiag"
    },
  ],
},
{
  title: "病歷借閱",
  name: "Ier2080"
},
{
  title: "雲端資料",
  name: "cloudData"
},
{
  title: "PACS系統",
  name: "pacsLink"
},
];


const otherMenu = [
  {
    title: "出院團隊衛教",
    name: "Comm6010"
  },
  {
    title: "出院團隊衛教範本",
    name: "Comm6011"
  }
]
export{
  menuOptions,
  otherMenu
}
```

