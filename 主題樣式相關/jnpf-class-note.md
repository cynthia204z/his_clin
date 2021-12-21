## 組件

### tab

```html
<el-tabs
         :lazy="true"
         v-model="activePane"
         type="border-card"
         class="JNPF-el_tabs oerpatbas oertabs"
         :class="{ 'change-tabsStyle': !styleStatus.patPanelIsShow }"
         >
  <el-tab-pane
               label="歷次就診記錄"
               name="1"
               style="width: 100%; background: #fff"
               class="JNPF-common-layout"
               >
  </el-tab-pane>
</el-tabs>
```



## table底線

```css
border-bottom: 1px solid #ebeef5 !important;
```



## 排版

### 0. class

JNPF-common-layout

JNPF-common-layout-main

JNPF-common-layout-center

JNPF-common-layout-left

### 1.

<img src="https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210819162028991.png" alt="image-20210819162028991" style="zoom:33%;" />

```html
<div class="JNPF-common-layout">
  <div class="JNPF-common-layout-center">
    <div class="center-content _top"></div>
    <div class="center-content"></div>
  </div>
  <div class="JNPF-common-layout-left panel-right"></div>
</div>
```





# 11/15 table border測試保留-------

```scss
th.is-leaf {
  border-bottom: $color 1px solid !important;
  border-right: none !important;
  &:not(:first-of-type){
   border-left: $color 1px solid;
  }
  border-top: $color 1px solid;
}
```



