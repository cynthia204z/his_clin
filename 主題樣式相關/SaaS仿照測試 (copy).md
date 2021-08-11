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

隱藏滾動條較乾淨。



**滾動**

☑ JNPF：系統管理/系統圖標

☐ SaaS：預約

切換標籤頁需要滾動回最上方較耗時。



**多頁簽**

☐ JNPF：系統管理/系統圖標

☑ SaaS：預約

顏色對比明顯，當前標籤頁較明顯。



**單元格狀態顯示**

☐ JNPF：醫院/科別數據維護/生效註記

☑ SaaS：在線問診/問診訂單管理/全部訂單/訂單狀態&付款狀態

色塊清楚區分現在狀態。



------

# 筆記

深紫 MENU色  #3E3D76

淺紫 主題色      #7D7AC1

灰 navbar色     #DADADA

深藍  線             #2C313C



------

# 源碼紀錄

<span id="jump">theme.scss  (這塊被取代成`@minix mixinSidebarBg`)</span>

```scss
/*end*/
#app .lightWhite {
  background-color: #fff !important; 
  .sidebar-logo-container {
    background: #fff !important;
    border-bottom: 1px solid #dcdfe6 !important;
  }

  &.sidebar-container {
    .el-menu {
      background: #fff;

      .el-submenu__title,
      .el-menu-item {
        color: #333;

        i {
          color: #666;
        }
      }
    }
  }

  & .nest-menu .el-submenu>.el-submenu__title,
  & .el-submenu .el-menu-item {
    background-color: #fff !important;
    color: #333;

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

------

# ==仿照SaaS 改動的地方==

## common.scss

> src/assets/scss/common.scss

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

* 暫時加的標題，不確定JNPF生出來的標題長怎樣

![image-20210614003210180](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210614003210180.png)

![image-20210614003344412](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210614003344412.png)

------

## sidebar.scss

> src/styles/sidebar.scss

##### 修改

###### 導覽列預設背景色

![image-20210612213424304](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210612213424304.png)

###### 導覽列選項高度

￼￼![image-20210611173404246](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611173404246.png)

------

## theme.scss

> src/styles/theme.scss

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

![image-20210612213620368](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210612213620368.png)

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

![image-20210613022542970](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210613022542970.png)

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

![image-20210615084413070](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210615084413070.png)

###### 原navbar修改

![jnpf前端theme scss修改](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/jnpf前端theme scss修改.png)

![image-20210611173758360](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210611173758360.png)

------

## JNPF-table/index.vue

> src/components/JNPF-table/index.vue

##### 增加

###### 表格斑馬紋

![image-20210612220333018](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210612220333018.png)

------

## tagsView/index.vue

> src/layout/components/tagsView/index.vue

##### 修改

###### 上方頁簽關閉icon

![image-20210615084948909](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210615084948909.png)

------

## setting/index.vue

> src/layout/components/setting/index.vue

##### 增加

###### 新增主題

data.imgUrl3

![image-20210612220040818](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210612220040818.png)

------

## zhtw.js

> src/lang/zhtw.js

##### 增加

###### 新增主題

![image-20210612220510547](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210612220510547.png)

------

## zh.js

> src/lang/zh.js

##### 增加

###### 新增主題

![image-20210612220604270](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210612220604270.png)

# 另外改/加的

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

------

# ==換logo的地方==

src/layout/classic/sidebar/Logo.vue

src/layout/plain/sidebar/Logo.vue

src/layout/functional/Logo.vue

