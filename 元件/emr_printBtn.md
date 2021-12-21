# 封裝

```vue
<template>
  <div class="print-btn">
    <el-dropdown split-button :type="type" @click="printDDclick(printDD)">
      <i style="font-size: 12px" class="ym-custom ym-custom-printer"></i>
      {{ printDD }}
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item
          v-for="(item, index) in printBtnData"
          :key="index"
          @click.native="printDropdownClick(item.label)"
        >{{item.label}}</el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
    <printerLocation1Dialog
      :printerLocation1DialogVisible="popup.printerLocation1DialogVisible"
      @close="popup.printerLocation1DialogVisible=false"
    ></printerLocation1Dialog>
  </div>
</template>
<script>
import { printBtnData1, printBtnData2 } from "@/views/his7/emr/utils/static";
import printerLocation1Dialog from "@/views/his7/emr/ierpat/dialog/printerLocation_1Dialog";
export default {
  components: {
    printerLocation1Dialog,
  },
  props: {
    default: {
      type: String,
      default: "門診列印",
    },
    hasPDF: {
      type: Boolean,
      default: true,
    },
    type: {
      type: String,
      default: "primary",
    },
  },
  data() {
    return {
      printBtnData: this.hasPDF ? printBtnData1 : printBtnData2,
      printDD: this.default,
      popup: {
        printerLocation1DialogVisible: false,
      },
    };
  },
  watch: {
    default: function (newVal, oldVal) {
      this.printDD = newVal;
    },
    hasPDF: function (newVal, oldVal) {
      if (newVal) {
        this.printBtnData = printBtnData1;
      } else {
        this.printBtnData = printBtnData2;
      }
    },
  },
  methods: {
    printDropdownClick(label) {
      this.printDD = label;
      this.printDDclick(this.printDD);
    },
    printDDclick(type) {
      if (type === "住院列印") {
        this.popup.printerLocation1DialogVisible = true;
      } else {
        this.$emit("printTable");
      }
    },

    print(id) {
      const tabStyle = `<style>
                table{width:100%;display:table-cell!important;box-sizing:border-box;}
                .el-table__header,.el-table__body,.el-table__footer{width:100%!important;border-collapse: collapse;text-align:center;}
                table, table tr td { border:1px solid #333;color:#606266;word-wrap:break-word}
                table tr th,table tr td{padding:4mm 0mm;word-wrap:break-word }
                table thead{border-bottom:0!important;display:none;}
                .el-table__body, tr td .cell{width:100%!important}
                .el-table th.gutter{display: none;}
                .el-table colgroup.gutter{display: none;}                
                </style><body>`;
      const html = document.querySelector("#" + id).innerHTML;
      // 新建一個 DOM
      const div = document.createElement("div");
      const printDOMID = "printDOMElement";
      div.id = printDOMID;
      div.innerHTML = html;
      // 提取第一個表格的內容 即表頭
      const ths = div.querySelectorAll(".el-table__header-wrapper th");
      const ThsTextArry = [];
      for (let i = 0, len = ths.length; i < len; i++) {
        if (ths[i].innerText !== "") ThsTextArry.push(ths[i].innerText);
      }
      // 刪除多餘的表頭
      div.querySelector(".hidden-columns").remove();
      //  刪掉第一個表格的內容
      div.querySelector(".el-table__header-wrapper").remove();
      //取出表頭放到tr裡面
      let newHTML = "<tr>";
      for (let i = 0, len = ThsTextArry.length; i < len; i++) {
        newHTML +=
          '<td style="text-align: center; font-weight: bold;padding:10px;">' +
          ThsTextArry[i] +
          "</td>";
      }
      newHTML += "</tr>";
      let printStr =
        "<html><head><meta http-equiv='Content-Type' content='text/html; charset=utf-8'></head>";
      let content = "";
      let print = document.getElementById(id).innerHTML;
      content = content + print;
      let content1 = content.replace("<tbody>", "<tbody>" + newHTML);
      let printPart1 = printStr + tabStyle + content1 + "</body></html>";
      let newTab = window.open("_blank");
      newTab.document.body.innerHTML = printPart1;
      newTab.focus();
      newTab.print();
      newTab.close();
    },
  },
};
</script>
<style lang="scss" scoped>
.print-btn {
  display: inline;
  margin-left: 10 px;
}
</style>
```

# 使用

```vue
<printBtn
          ref="printBtn"
          default="門診列印"
          :hasPDF="false"
          @printTable="$refs['printBtn'].print('emrlisresult')"
          ></printBtn>

<!---->
<JNPF-table id="emrlisresult"></JNPF-table>
```

