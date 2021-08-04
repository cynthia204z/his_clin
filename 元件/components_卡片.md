



# 橫式病患卡片 PatCard

## 1. 一張卡片

![image-20210713084851872](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210713084851872.png)

```html
<PatCard :data="patCardItem" :No="1" :hasFooter="false">
  <!--v-slot:head-->
  <!--v-slot:footer-->
</PatCard>
```
```json
patCardItem: {
  status: "status",
  statusStyle: "yellow",
  patName: "王小姐",
  birthDate: "2000-10-17",
  sexType: "女",
  details: [
    {
      label: "病歷號碼",
      value: undefined,
    },
    {
      label: "証號",
      value: undefined,
      disc: "身分證",
    },
    {
      label: "生日",
      value: undefined,
    },
  ],
},
```

### 參數說明

#### `<PatCard>`標籤屬性

==Attributes==

| **參數**  | **說明**                 | **類型** | **可選值** | **預設值** |
| --------- | ------------------------ | -------- | ---------- | ---------- |
| data      | 資料來源                 | object   | -          | -          |
| hasFooter | 是否顯示卡片下方區塊     | boolean  | -          | true       |
| No        | 序號，不帶此屬性則不顯示 | number   | -          | -          |
| fontSize  | 字型大小                 | string   | sm/md/lg   | md         |

#### data欄位

==data Attributes==

| **欄位**    | **說明**                                         | **類型**        | **可選值**            | **預設值** |
| ----------- | ------------------------------------------------ | --------------- | --------------------- | ---------- |
| status      | 狀態文字內容，不帶此屬性則不顯示(頭像下方圓角框) | string / number | -                     | -          |
| statusStyle | 卡片左側樣式                                     | string          | red/blue/green/yellow | -(主題色)  |
| patName     | 病患姓名                                         | string          | -                     | -          |
| birthDate   | 年齡(可傳生日或年齡)，不帶此屬性則不顯示         | string / number | -                     | -          |
| sexType     | 性別，不帶此屬性則不顯示                         | string / number | -                     | -          |
| details     | 卡片文字內容設定                                 | array           | -                     | -          |

#### 卡片文字內容(details)欄位

==details-item Attributes==

| **欄位** | **說明**                     | **類型**        | **可選值** | **預設值** |
| -------- | ---------------------------- | --------------- | ---------- | ---------- |
| label    | 欄位標題文字                 | string / number | -          | -          |
| value    | 欄位值文字                   | string / number | -          | -          |
| disc     | 註解文字，不帶此屬性則不顯示 | string / number | -          | -          |

### 插槽使用範例

![image-20210712222227218](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210712222227218.png)

![image-20210713085149268](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210713085149268.png)

#### 插槽說明： ==Slot==

| **name** | **說明**                                                     |
| -------- | ------------------------------------------------------------ |
| head     | 卡片上方(姓名性別歲數)右側插槽                               |
| headInfo | 自訂資訊：卡片上方姓名性別右側插槽，建議只放文字             |
| status   | 自訂狀態：可以不使用data.status，使用具名插槽方便渲染動態資料；<br />也可以都使用，將得到兩個狀態框。 |
| footer   | 卡片下方區塊的內容                                           |
| —        | details區塊(卡片中間)匿名插槽                                |

#### - 具名插槽

> 具名插槽請用 template 標籤包起來

```html
<PatCard :data="item" :No="index">
  <!--v-slot:head-->
  <template v-slot:head>
    <el-button type="text">
      <i class="el-icon-phone card-icon"></i>
    </el-button>
  </template>
  <!--v-slot:footer-->
  <template v-slot:footer>
    <el-button class="card-btn" @click="addOrUpdateHandle(item.id)">詳情</el-button>
    <el-button class="card-btn">退號</el-button>
    <el-button class="card-btn">叫號</el-button>
    <el-dropdown class="card-btn">
      <el-button style="width:100%;height:100%">
        更多操作
        <i class="el-icon-arrow-down el-icon--right"></i>
      </el-button>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item>更多操作1</el-dropdown-item>
        <el-dropdown-item>更多操作2</el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
  </template>
</PatCard>
```

```json
patCardItem: {
  status: "status",
  statusStyle: "red",
  patName: "",
  birthDate: undefined,
  sexType: undefined,
  details: [
    {
      label: "病歷號碼",
      value: undefined,
    },
    {
      label: "証號",
      value: undefined,
      disc: "身分證",
    },
    {
      label: "生日",
      value: undefined,
    },
  ],
},
```



#### - 匿名插槽

![image-20210713085608238](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210713085608238.png)

```html
<PatCard :data="patCardItem" :No="1" :hasFooter="false">
  <el-button type="primary">匿名插槽</el-button>
</PatCard>
```



### 7/21 補充&新增功能

1. 卡片內容不使用組件的包裝的話(例如需要動態渲染)，可以以下列標籤格式直接放在原本的匿名插槽

```html
<span class="card-item card-item-left">
  {{ 標題 }}&nbsp;
  <p>{{ 內容 }}</p>
  <p style="color:red">({{ 補充說明/狀態等等 }})</p>
</span>
```
2. 性別、歲數或更多自訂卡片上方資訊可以選擇不要用欄位帶進去，用具名插槽`v-slot:headInfo`
3. 年齡可以直接放歲數進去了



### 7/22  新增

新增具名插槽`v-slot:status`

![image-20210722101914734](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210722101914734.png)

```html
<template v-slot:status>文字</template>
```



### 8/4 字型大小

`fontSize="lg"`、`fontSize="md"`、`fontSize="sm"`

使用範例：

```html
<PatCard :data="item" fontSize="lg"></PatCard>
```

> 如果卡片內容使用插槽 (見**7/21 補充&新增功能**)，請手動加入樣式類別，範例如下：
>
> ```html
> <PatCard :data="item" fontSize="lg">
>   <span class="card-item card-item-left lg">
>     {{ 標題 }}&nbsp;
>     <p>{{ 內容 }}</p>
>     <p style="color:red">({{ 補充說明/狀態等等 }})</p>
>   </span>
> </PatCard>
> ```

lg   ( font-size : 14px )

![image-20210804191759613](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210804191759613.png)

md  ( font-size : 13px )

![image-20210804192758607](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210804192758607.png)

sm   ( font-size : 12px )

![image-20210804192151639](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210804192151639.png)





## 2. Card Page 範例

![image-20210722103157097](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210722103157097.png)

```html
<template>
  <div class="JNPF-common-layout">
    <div class="JNPF-common-layout-center">
      <el-row class="JNPF-common-search-box" :gutter="16">
        ...
      </el-row>

      <div class="JNPF-common-layout-main JNPF-flex-main" v-loading="loading">

        <!-- 外層樣式 card-page card-area flex-warp 已定義在scss可以直接使用-->
        <div class="card-page">
          <el-row :gutter="12" class="card-area flex-warp" type="flex">
            <el-col
                    class="card-col"
                    :xs="24"
                    :sm="24"
                    :md="12"
                    :lg="8"
                    :xl="8"
                    v-for="(item, index) in patCardList"
                    :key="index"
                    >
              <PatCard :data="item" :No="index + 1">
                <!-- 具名插槽status -->
                <template v-slot:status>文字</template>
                <!-- 具名插槽headInfo -->
                <template v-slot:headInfo>
                  {{ item.mobile || "無資料" }}
                </template>
                <!-- 具名插槽head -->
                <template v-slot:head>
                  <el-tooltip
                              class="item"
                              effect="dark"
                              :content="item.mobile || '無資料'"
                              placement="top"
                              >
                    <el-button type="text">
                      <i class="el-icon-phone card-icon"></i>
                    </el-button>
                  </el-tooltip>
                </template>
                <!-- 具名插槽footer -->
                <template v-slot:footer>
                  <el-button
                             class="card-btn"
                             @click="addOrUpdateHandle(item.id)"
                             >詳情</el-button
                    >
                  <el-button class="card-btn">退號</el-button>
                  <el-button class="card-btn">叫號</el-button>
                  <el-dropdown class="card-btn">
                    <el-button style="width: 100%; height: 100%">
                      更多操作
                      <i class="el-icon-arrow-down el-icon--right"></i>
                    </el-button>
                    <el-dropdown-menu slot="dropdown">
                      <el-dropdown-item>更多操作1</el-dropdown-item>
                      <el-dropdown-item>更多操作2</el-dropdown-item>
                    </el-dropdown-menu>
                  </el-dropdown>
                </template>
                <!-- 匿名插槽 -->
                <span class="card-item card-item-left">
                  標題 &nbsp;
                  <p> 內容 </p>
                  <p style="color: red">( 補充說明 / 狀態等等 )</p>
                </span>
                <span class="card-item card-item-left">
                  標題 &nbsp;
                  <p> 內容 </p>
                </span>
              </PatCard>
            </el-col>
          </el-row>
        </div>
      </div>

      <pagination .../>
    </div>
    <JNPF-Form v-if="formVisible" ref="JNPFForm" @refresh="refresh" />
  </div>
</template>
<script>
  import request from "@/utils/request";
  import JNPFForm from "./Form";

  export default {
    components: { JNPFForm },
    data() {
      return {
        // 此範例僅列出與頁面中PatCard相關的方法
        list: [],
        patCardList: [],
        patCardItem: {
          // status: "status",
          patName: "王小明",
          birthDate: undefined,
          sexType: undefined,
          mobile: undefined,
          id: undefined,
          details: [
            {
              label: "病歷號碼",
              value: undefined,
            },
            {
              label: "証號",
              value: undefined,
              disc: "身分證",
            },
            {
              label: "生日",
              value: undefined,
            },
          ],
        },
      };
    },
    created() {
      this.$nextTick(() => {
        this.initData();
      });
    },
    methods: {
      // 此範例僅列出與頁面中PatCard相關的方法
      initData() {
        this.loading = true;
        this.patCardList = [];
        let _query = {
          ...this.listQuery,
          ...this.query,
        };
        let query = {};
        for (let key in _query) {
          if (Array.isArray(_query[key])) {
            query[key] = _query[key].join();
          } else {
            query[key] = _query[key];
          }
        }
        request({
          url: `/api/his7/com/chartinfo/ComChrbas`,
          method: "get",
          data: query,
        }).then((res) => {
          this.list = res.data.list;
          for (let i = 0; i < this.list.length; i++) {
            this.list[i].birthDate = this.$moment(this.list[i].birthDate).format(
              "YYYY-MM-DD"
            );
            this.patCardItem.id = this.list[i].id;
            this.patCardItem.patName = this.list[i].patName;
            this.patCardItem.birthDate = this.list[i].birthDate;
            this.patCardItem.mobile = this.list[i].mobile;
            this.patCardItem.sexType = this.list[i].sexType;
            this.patCardItem.details[0].value = this.list[i].chartNo;
            this.patCardItem.details[1].value = this.list[i].idNo;
            this.patCardItem.details[2].value = this.list[i].birthDate;
            this.patCardList.push(this.patCardItem);
            this.patCardItem = {
              // status: "status",
              patName: "",
              birthDate: undefined,
              sexType: undefined,
              mobile: undefined,
              id: undefined,
              details: [
                {
                  label: "病歷號碼",
                  value: undefined,
                },
                {
                  label: "証號",
                  value: undefined,
                  disc: "身分證",
                },
                {
                  label: "生日",
                  value: undefined,
                },
              ],
            };
          }
          this.total = res.data.pagination.total;
          this.loading = false;
        });
      },
    },
  };
</script>
```



# 直式病患卡片 PatPanel

![image-20210713093720446](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210713093720446.png)

```html
<!-- 卡片外框+基本資料 -->
<PatPanel :data="panelText" :patInfo="patInfo">
  <!-- DATE TYPE -->
  <PatPanel-block type="date" :dateText="blockText"></PatPanel-block>
  <PatPanel-block :data="panelBlockData1"></PatPanel-block>
  <PatPanel-block :data="panelBlockData2"></PatPanel-block>
</PatPanel>
```

```js
export default {
  data() {
    return {
      // 基本資料
      panelText: {
        patName: "王小明",
        sex: "男",
        status1: "status",
        birthDate: "1996-12-31",
        mobile: undefined,
      },
      // 更多病患資訊(年齡手機下方)
      patInfo: [
        {
          icon: "icon-ym icon-ym-extend-bus",
          text: "其他資訊1",
        },
        {
          icon: "icon-ym icon-ym-xingcheng",
          text: "其他資訊2",
        },
      ],
      // type = "date" 的資料格式
      // 但不一定要放日期，也可以放別的內容
      blockText: [
        {
          label: "AA日期",
          value: "2021-06-16",
        },
        {
          label: "BB日期",
          value: "2021-07-16",
        },
      ],
      panelBlockData1: [
        {
          title: "標題1",
        },
        {
          title: "標題2",
        },
      ],
      panelBlockData2: [
        {
          title: "標題3",
          details: [
            {
              label: "小標題1",
              value: "內容",
            },
            {
              label: "小標題2",
              value: "內容",
              disc: "註解",
            },
            {
              label: "小標題3",
              value: "內容",
            },
          ],
        },
        {
          title: "標題4",
          details: [
            {
              label: "小標題1",
              value: "內容",
            },
            {
              label: "小標題2",
              value: "內容",
            },
          ],
        },
      ],
    };
  },
};
```
## PatPanel

> 卡片外框

### 參數說明

#### ==Patpanel Attributes==

| **參數** | **說明**         | **類型** | **可選值** | **預設值** |
| -------- | ---------------- | -------- | ---------- | ---------- |
| data     | 資料來源         | object   | -          | -          |
| photo    | 是否顯示圖片區域 | boolean  | -          | true       |
| patInfo  | 其他病患資訊設定 | array    | -          | -          |

#### ==Patpanel data Attributes==

| **欄位**  | **說明**                                                   | **類型**        | **可選值** | **預設值** |
| --------- | ---------------------------------------------------------- | --------------- | ---------- | ---------- |
| status1   | 狀態文字內容，不帶此屬性則不顯示(姓名右側)                 | string / number | -          | -          |
| status2   | 狀態文字內容，不帶此屬性則不顯示(姓名右側)                 | string / number | -          | -          |
| patName   | 病患姓名                                                   | string          | -          | -          |
| sexType   | 性別                                                       | string / number | -          | -          |
| birthDate | 帶入生日顯示年齡，不帶此屬性則不顯示(頭像姓名下方病患資訊) | string / number | -          | -          |
| mobile    | 手機號碼，不帶此屬性則不顯示(頭像姓名下方病患資訊)         | string / number | -          | -          |

#### ==Patpanel patInfo Attributes==

| **欄位** | **說明**          | **類型** | **可選值** | **預設值** |
| -------- | ----------------- | -------- | ---------- | ---------- |
| icon     | 圖示的 class name | string   | -          | -          |
| text     | 文字              | string   | -          | -          |

## PatPanel-block

> 卡片內容區塊 

![image-20210713094359904](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210713094359904.png)

### 參數說明

#### ==Patpanel-block Attributes==

| **參數** | **說明**                  | **類型** | **可選值** | **預設值** |
| -------- | ------------------------- | -------- | ---------- | ---------- |
| type     | 類型                      | string   | date       | -          |
| dateText | 日期標題與文字內容設定    | object   | -          | -          |
| data     | 非date類型的block資料來源 | object   | -          | -          |

#### ==Patpanel-block dateText-item Attributes==

| **欄位** | **說明**     | **類型**        | **可選值** | **預設值** |
| -------- | ------------ | --------------- | ---------- | ---------- |
| label    | 欄位標題文字 | string / number | -          | -          |
| value    | 欄位值文字   | string / number | -          | -          |

#### ==Patpanel-block data-item Attributes==

| **欄位** | **說明**                           | **類型**        | **可選值** | **預設值** |
| -------- | ---------------------------------- | --------------- | ---------- | ---------- |
| name     | 自定義內容(slot)需使用到的區塊名稱 | string          | -          | -          |
| title    | 標題文字                           | string / number | -          | -          |
| details  | 詳細內容                           | array           | -          | -          |

#### ==Patpanel-block details-item Attributes==

| **欄位** | **說明**                     | **類型**        | **可選值** | **預設值** |
| -------- | ---------------------------- | --------------- | ---------- | ---------- |
| label    | 欄位標題文字                 | string / number | -          | -          |
| value    | 欄位值文字                   | string / number | -          | -          |
| disc     | 註解文字，不帶此屬性則不顯示 | string / number | -          | -          |

## 插槽使用範例

![image-20210713092313978](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210713092313978.png)

```html
<PatPanel :data="panelText" :patInfo="patInfo">
  <PatPanel-block type="date" :dateText="blockText"></PatPanel-block>
  <PatPanel-block :data="panelBlockData1">
    <!-- 具名插槽範例 -->
    <template v-slot:titleName1-title>
      <el-button type="text" @click="btn1ClickEvent">
        按鈕<i class="el-icon-edit" />
      </el-button>
    </template>
    <!-- 具名插槽範例 -->
    <template v-slot:titleName1-content>
      <el-input placeholder="自定義內容" size="mini" controls-position="right" />
    </template>
    <!-- 具名插槽範例 -->
    <template v-slot:titleName2-content>
      <span>自定義內容自定義內容自定義內容自定義內容</span>
    </template>
  </PatPanel-block>
  <PatPanel-block :data="panelBlockData2">
    <!-- 具名插槽範例 -->
    <template v-slot:titleName3-content>
      <el-button type="primary" @click="btn1ClickEvent">
        <i class="icon-ym icon-ym-generator-function" />自定義內容
      </el-button>
    </template>
    <!-- 具名插槽範例 -->
    <template v-slot:titleName4-title>
      <el-button type="text" @click="btn1ClickEvent">
        <i class="el-icon-edit" />
      </el-button>
    </template>
    <!-- 匿名插槽 -->
    <span>最下方匿名插槽</span>
  </PatPanel-block>
</PatPanel>
```

```js
export default {
  data() {
    return {
      // 基本資料
      panelText: {
        patName: "王小明",
        sex: "男",
        status1: "status",
        birthDate: "1996-12-31",
        mobile: undefined,
      },
      // 更多病患資訊(年齡手機下方)
      patInfo: [
        {
          icon: "icon-ym icon-ym-extend-bus",
          text: "其他資訊1",
        },
        {
          icon: "icon-ym icon-ym-xingcheng",
          text: "其他資訊2",
        },
      ],
      blockText: [
        {
          label: "AA日期",
          value: "2021-06-16",
        },
        {
          label: "BB日期",
          value: "2021-07-16",
        },
      ],
      panelBlockData1: [
        {
          name: "titleName1", //插槽用名稱，不使用插槽則可不寫
          title: "標題1",
        },
        {
          name: "titleName2", //插槽用名稱
          title: "標題2",
        },
      ],
      panelBlockData2: [
        {
          name: "titleName3", //插槽用名稱
          title: "標題3",
          details: [
            {
              label: "小標題1",
              value: "內容",
            },
            {
              label: "小標題2",
              value: "內容",
              disc: "註解",
            },
            {
              label: "小標題3",
              value: "內容",
            },
          ],
        },
        {
          name: "titleName4", //插槽用名稱
          title: "標題4",
          details: [
            {
              label: "小標題1",
              value: "內容",
            },
            {
              label: "小標題2",
              value: "內容",
            },
          ],
        },
      ],
    };
  },
};
```
### 插槽說明： ==Patpanel-block Slot==

| **name**     | **說明**                       |
| ------------ | ------------------------------ |
| name-title   | 標題右側插槽                   |
| name-content | 自定義內容(title、details下方) |
| —            | 最下方匿名插槽                 |
