# SaaS 整體優點

- 區塊較分明
- **卡片化**：符合現代人使用習慣

- 左邊線凸顯標題，增加區塊辨識度。

------

# SaaS JNPF比較

**Details返回鍵 **

☑ JNPF：

☐ SaaS：掛號/掛號列表/卡片詳情

多數app與網頁返回鍵都在左側，使用者下意識往左側找的機會較大。



**MENU**

☑ JNPF

☐ SaaS

標題和LOGO不應該跟MENU一起滑動。

隱藏滾動條畫面較乾淨。



**滾動**

☑ JNPF：系統管理/系統圖標

☐ SaaS：預約

切換標籤頁需要滾動回最上方較耗時。



**多頁簽**

☐ JNPF：系統管理/系統圖標

☑ SaaS：預約

顏色對比明顯，當前標籤頁較醒目。



**單元格狀態顯示**

☐ JNPF：醫院/科別數據維護/生效註記

☑ SaaS：在線問診/問診訂單管理/全部訂單/訂單狀態&付款狀態

色塊清楚區分現在狀態。



------

# SaaS 顏色紀錄

深紫 MENU色  #3E3D76

淺紫 主題色      #7D7AC1

灰 navbar色     #DADADA

深藍  線             #2C313C



------

# 6/11 臨時筆記區

```css
// 沒打開的選項
#app .lightWhite.sidebar-container .el-menu{
	background:red;
}
#app .sidebar-container .el-menu{
	background:;
}
.el-menu{
    background-color:;
}
// 底色
#app .sidebar-container{
	background-color:;
} 
```

------

# 6/12 臨時筆記區

```
// theme color
$purple: #722ED1;
$purpleSub: #C34AFF;
$azure: #211BCE;
$azureSub: #4D89F1;
$blackblue:#211BCE;
$blackblueSub:#4D89F1;
$blue:#1890ff;
$blueSub:#3FB9F8;
$ocean:#13C2C2;
$oceanSub:#69D5E6;
// $green: #3EAC12;
// $greenSub: #5BDECC;  自己改了個順眼一點的綠色#
$green: #7ac1a9;
$greenSub: #3d7668;
$yellow: #F8BC18;
$yellowSub: #FF9C1C;
$orange: #F5811C;
$orangeSub: #FEB814;
$red: #F5222D;
$redSub: #FF5D65;
// 6/11 仿照SaaS測試
$saastest: #7D7AC1;
$saastestSub: #3E3D76;
```



<span id="jump">theme.scss     6/11版  (這塊被取代成`@minix mixinSidebarBg`)</span>

```scss
/* 6/12 加 start*/
#app .dark{
  &.sidebar-container{
    background: #031425;
  }
}
/*end*/
#app .lightWhite {
  // background-color: #fff !important; 
  .sidebar-logo-container {
    background: #fff !important;
    border-bottom: 1px solid #dcdfe6 !important;
  }

  &.sidebar-container {
    .el-menu {
      background: #fff;
      // background: #3E3D76;

      .el-submenu__title,
      .el-menu-item {
        color: #333;
        // color: #fff;

        i {
          color: #666;
          // color: #fff;
        }
      }
    }
  }

  & .nest-menu .el-submenu>.el-submenu__title,
  & .el-submenu .el-menu-item {
    background-color: #fff !important;
    // background-color: #3E3D76;
    color: #333;
    // color: #fff;

    &:hover {
      color: #1890ff;
      background-color: transparent;

      i {
        color: #1890ff;
      }
    }

    &.is-active {
      background-color: #1890ff !important;
    }
  }
}
```

表單標題備份

```scss
// .groupTitle font font{
//   border-left: 6px solid #7D7AC1;
//   padding-left: 10px;
//   font-weight: 600;
// }
```

------

# 6/11 仿照測試

## src/assets/scss/common.scss

![image-20210611173109742](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611173109742.png)

## src/styles/sidebar.scss

![image-20210624234359999](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624234359999.png)

## src/styles/theme.scss

![image-20210611173502460](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611173502460.png)

![image-20210611173611184](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611173611184.png)

![image-20210611173643480](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611173643480.png)

![image-20210624234334937](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624234334937.png)

![image-20210611174508051](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174508051.png)

![image-20210611173923567](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611173923567.png)

![image-20210611174135071](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174135071.png)

![image-20210611174204629](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174204629.png)

![image-20210611174250829](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174250829.png)

![image-20210611174324401](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174324401.png)

![image-20210611174603744](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174603744.png)

![image-20210611174637541](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174637541.png)

![image-20210611174700801](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174700801.png)

```scss
#app .saastest {
  @include mixinNavbar($saastest, $saastestSub);
  @include mixinCommon($saastest, $saastestSub);
  @include mixinSidebar($saastest, $saastestSub);
  @extend .ligthNavbar;
}

.saastest {
  @include mixinPopup($saastest);
}
```

## 暫時增加的CSS

![image-20210611174752558](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174752558.png)

![image-20210611174815500](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174815500.png)

![image-20210611174829989](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174829989.png)

![image-20210611174848337](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611174848337.png)

## 備份

```scss
// tab 標籤樣式
.el-tabs--border-card > .el-tabs__header .el-tabs__nav-scroll {
  background: #7D7AC1 !important;
}


/*標籤*/
.el-tabs--border-card > .el-tabs__header .el-tabs__item {
  background: #7D7AC1 !important;
  border: none;
  border-bottom: none !important;
  color: #fff !important;
  transition: none !important;
}
.el-tabs--border-card > .el-tabs__header .el-tabs__item:hover {
  background: #7D7AC1 !important;
}

/*選中的標籤*/
.el-tabs--border-card > .el-tabs__header .el-tabs__item.is-active {
  background: #fff !important;
  z-index: 2;
  color: #7D7AC1 !important;
  ont-weight: 800;
}
.el-tabs--border-card > .el-tabs__header .el-tabs__item.is-active:hover{
  background: #fff !important;
  cursor: default;
}
.el-tabs--border-card > .el-tabs__header .el-tabs__item.is-active:before{
  content: "";
  position: absolute;
  border-bottom: 40px solid #fff;
  border-left: 10px solid transparent;
  left: -10px;
}
.el-tabs--border-card > .el-tabs__header .el-tabs__item.is-active:after{
  content: "";
  position: absolute;
  border-bottom: 40px solid #fff;
  border-right: 10px solid transparent;
  right: -10px;
}
.el-tabs--border-card > .el-tabs__header .el-tabs__nav {
  border: none !important;
  border-bottom: none;
}
.el-tabs--border-card > .el-tabs--card>.el-tabs__header{
  border: none !important;
}

```

```scss
// side menu
#app .sidebar-container{
  background-color: #3E3D76 !important;
}

// 選項hover
.el-menu .el-submenu__title:hover,
.el-menu .el-menu .el-menu-item:hover {
  background-color: #7D7AC1 !important;
  color: #fff !important;
}

// 選項hover時的icon
.el-menu .el-submenu__title:hover .icon-ym:before,
.el-menu .el-menu .el-menu-item:hover .icon-ym:before,
.el-menu .el-submenu__title:hover .ym-custom:before,
.el-menu .el-menu .el-menu-item:hover .ym-custom:before,
.el-menu .el-submenu__title:hover .el-icon-arrow-down:before,
.el-menu .el-menu .el-menu-item:hover .el-icon-arrow-down:before {
  color: #fff !important;
}

.el-menu .el-menu .el-menu-item,
.el-menu .el-submenu__title {
  color: #e9e3ef !important;  //這行還沒加
  background-color: #3E3D76 !important;
}
```



# ==6/12 仿照SaaS完整版==

(6/11的不用看 直接看6/12重新整理的)

### src/assets/scss/common.scss

##### 增加

###### 標籤頁樣式

```scss
// main 區塊 標籤頁
.el-tabs--border-card{
  border: none !important;

  > .el-tabs__header{

    .el-tabs__item{
      transition: none !important;
      border: none;
      border-bottom: none !important;

      &.is-active{
        font-weight: 800;
        z-index: 2;
        &:hover{
          cursor: default;
        }
        &:before{
          content: "";
          position: absolute;
          border-bottom: 40px solid #fff;
          border-left: 10px solid transparent;
          left: -10px;
        }
        &:after{
          content: "";
          position: absolute;
          border-bottom: 40px solid #fff;
          border-right: 10px solid transparent;
          right: -10px;
        }
      }

      .el-tabs__nav {
        border: none !important;
        border-bottom: none;
      }
    }
  }

  > .el-tabs--card{
    > .el-tabs__header{
      border: none !important;
    }
  }
}
```

###### 表單標題

```scss
//Form標題左邊線
.groupTitle{
  font-weight: 600;
}
.groupTitle:before{
  content: "";
  margin-right: 10px;
  height: 25px;
  line-height: 25px;
}
```

暫時加的標題，不確定JNPF生出來的標題長怎樣

![image-20210624234305392](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624234305392.png)

![image-20210624234247755](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624234247755.png)

------

### src/styles/sidebar.scss

##### 修改

###### 導覽列預設背景色

![image-20210624234227620](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624234227620.png)

###### 導覽列選項高度

![image-20210624234209869](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624234209869.png)

------

### src/styles/theme.scss

##### 增加

###### 標籤頁顏色

```scss
@mixin mixinTab($color) {
  // 主要內容區的標籤頁
  .el-tabs--border-card{
    > .el-tabs__header{

      // 底色
      .el-tabs__nav-scroll {
        background: $color !important;
      }

      // 標籤
      .el-tabs__item{
        background: $color !important;
        color: #fff !important;
        
        &:hover{
          background: $color !important;
        }
        &.is-active{
          background: #fff !important;
          color: $color !important;
          &:hover{
            background: #fff !important;
          }
        }
      }
    }
  }
}
```
###### 表單標題

```scss
@mixin mixinForm($color) {
  .groupTitle:before{
    border-left: 6px solid $color;
  }
}
```



###### 新增主題

![image-20210624234147332](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624234147332.png)

```scss
#app .saastest {
  @include mixinNavbar($saastest, $saastestSub);
  @include mixinCommon($saastest, $saastestSub);
  @include mixinSidebar($saastest);
  @include mixinTab($saastest);
  @include mixinSidebarBg($saastest, $saastestSub);
  @include mixinForm($saastest);
  @extend .ligthNavbar;
}

.saastest {
  @include mixinPopup($saastest);
}
```

![image-20210624234057540](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624234057540.png)

##### 修改

[點這連結到被取代掉的地方](#jump)

###### 左側導覽列

```scss
// 左側導覽列
@mixin mixinSidebarBg($color, $subColor) {
  .dark,
  .lightWhite{

    .sidebar-logo-container {
      background: $subColor !important;
      border-bottom: 1px solid #2C313C !important;
    }

    &.sidebar-container {
      background: $subColor !important;
      .el-menu {
        background: $subColor !important;

        .el-submenu__title,
        .el-menu-item {
          color: #fff;

          i {
            color: #fff;
          }
          &:hover{
            background-color: $color !important;
            color: #fff !important;

            .left-icon{
              &:before{
                color: #fff !important;
              }
            }
          }
          &.is-active {
            background-color: $color !important;
          }
        }

        .el-menu{
          .el-menu-item{
            &:hover{
              background-color: $color !important;
              color: #fff !important;
            }
          }
        }
      }
    }

    & .nest-menu .el-submenu>.el-submenu__title,
    & .el-submenu .el-menu-item {
      background-color: $subColor;
      color: #fff;

      &:hover {
        color: #1890ff;
        background-color: transparent;

        i {
          color: #1890ff;
        }
      }

      &.is-active {
        background-color: #1890ff !important;
      }
    }
  }
}
```

###### 上方頁簽

![image-20210624234034100](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624234034100.png)

###### 原navbar修改

![jnpf前端theme scss修改](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/jnpf前端theme scss修改.png)

![image-20210624234012873](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624234012873.png)

------

### src/components/JNPF-table/index.vue

##### 增加

###### 表格斑馬紋

![image-20210624233951152](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624233951152.png)

------

### src/layout/components/tagsView/index.vue

##### 修改

上方頁簽關閉icon

![image-20210624233929127](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624233929127.png)

------

### src/layout/components/setting/index.vue

##### 增加

###### 新增主題

data.imgUrl3

![image-20210624233912175](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624233912175.png)

------

### src/lang/zhtw.js

##### 增加

###### 新增主題

![image-20210624233853832](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624233853832.png)

------

### src/lang/zh.js

##### 增加

###### 新增主題

![image-20210624233830812](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210624233830812.png)



# 試加 彈窗標題樣式

彈窗的關閉按鈕垂直置中

![image-20210614011235056](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210614011235056.png)

```scss
// 我放在 @mixin mixinForm裡

/*彈窗標題 試加樣式(saas沒有自己加加)  start*/
  .JNPF-dialog {
    &.JNPF-dialog_center {
  
      .el-dialog {
  
        .el-dialog__header {
          background: $color;
          .el-dialog__title {
            color: #fff;
          }
        }
        
        .el-dialog__close {
          color: #fff;
        }
      }
    }
  }
  /*彈窗標題 試加樣式 end*/
```



# ==換logo的地方==

src/layout/classic/sidebar/Logo.vue

src/layout/plain/sidebar/Logo.vue

src/layout/functional/Logo.vue



# ==6/17 去標籤頁底線==

common.scss

![image-20210617201446797](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210617201446797.png)





# ==6/23 表格input樣式==

### src/assets/scss/common.scss

修+增

```scss
// 6/23 修改
.el-table__row .el-input {
  // &:hover{
  //   .el-input__inner{
  //     border-bottom: 1px solid #7ac1a9;
  //   }
  // }
  .el-input__inner{
    border-style: solid;
    border-color: transparent;
    border-radius: 0;
    background-color: transparent;
    transition: none;
    // &:focus{
    //   border-bottom: 1px solid #3d7668 !important;
    // }
  }
}

.el-table__row {
  .cell:hover .el-input-number{
    // .el-input__inner{
    //   border-bottom: 1px solid #7ac1a9;
    // }
    .el-input-number__increase,
    .el-input-number__decrease {
      display:inline;
    }
  }
  .el-input-number{
    .el-input-number__increase,
    .el-input-number__decrease {
      border-left: none !important;
      border-bottom: none !important;
      background: none;
    }
    .el-input-number__decrease:hover:not(.is-disabled)~.el-input .el-input__inner:not(.is-disabled),
    .el-input-number__increase:hover:not(.is-disabled)~.el-input .el-input__inner:not(.is-disabled){
      border-top: 1px solid transparent;
      border-right: 1px solid transparent;
      border-left: 1px solid transparent;
      // border-bottom: 1px solid #3d7668;
    }
    .el-input__inner{
      transition: none;
      // &:focus{
      //   border-bottom: 1px solid #3d7668 !important;
      // }
    }
  }
}

// .el-table__row .el-input .el-input__inner{
// border-style: none;
// }

// .hover-row .el-input .el-input__inner{
//   border-style:solid;
// }

.el-table__row .el-input-number__increase {
  display:none;
}
// .hover-row .el-input-number__increase {
//   display:inline;
// }

.el-table__row .el-input-number__decrease {
  display:none;
}
// .hover-row .el-input-number__decrease {
//   display:inline;
// }
```



### src/styles/theme.scss

增

```scss
// 6/23 input樣式
@mixin  mixinTableInput($color, $subColor) {
  .el-table__row .el-input {
    &:hover{
      .el-input__inner{
        border-bottom: 1px solid $color;
      }
    }
    .el-input__inner{
      &:focus{
        border-bottom: 1px solid $subColor !important;
      }
    } 
  }
  .el-select{
    &:hover .el-input__inner{
      border-color: transparent !important;
      border-bottom: 1px solid $color !important;
    }
    .el-input.is-focus .el-input__inner{
      border-color: transparent !important;
      border-bottom: 1px solid $subColor !important;
    }
    .el-input__inner:focus{
      border-color: transparent !important;
    }
  }
  
  .el-table__row {
    .cell:hover .el-input-number{
      .el-input__inner{
        border-bottom: 1px solid $color;
      }
    }
    .el-input-number{
      .el-input-number__decrease:hover:not(.is-disabled)~.el-input .el-input__inner:not(.is-disabled),
      .el-input-number__increase:hover:not(.is-disabled)~.el-input .el-input__inner:not(.is-disabled){
        border-bottom: 1px solid $subColor;
      }
      .el-input__inner{
        &:focus{
          border-bottom: 1px solid $subColor !important;
        }
      }
    }
  }
}
```

```scss
// 加 @include mixinTableInput($saastest, $saastestSub);
#app .saastest {
  @include mixinNavbar($saastest, $saastestSub);
  @include mixinCommon($saastest, $saastestSub);
  @include mixinSidebar($saastest);
  @include mixinTab($saastest);
  @include mixinSidebarBg($saastest, $saastestSub);
  @include mixinForm($saastest);
  @include mixinTableInput($saastest, $saastestSub);
  @extend .lightNavbar;
}s
```





# ==6/24 Card修改==

card-container 的 background 搬去 card（不然換比例就露白）

```scss
.card {
  background: rgb(248, 248, 248);
  border: 1px solid #dadada;
  min-width: 350px;
}

.card-container {
  padding: 10px;
  margin-right: 0;
  width: calc(100% - 100px);
  height: 100%;
}
```

