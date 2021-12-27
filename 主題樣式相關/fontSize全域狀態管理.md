# element UI 預設CSS變數

**Default**

node_modules/element-ui/packages/theme-chalk/src/common/var.scss

> 參考文章：[Vue Element-ui 全局變數](https://www.getit01.com/p20190218354835393/)



**自定義覆蓋**

src/styles/element-variables.scss



# 實現全域字型大小切換

## JNPF

### Default Setting

src/settings.js

```js
module.exports = {
  // ...
  fontSizeClass: 'mini'
}
```



### Store

src/store/modules/settings.js

```js
import variables from '@/styles/element-variables.scss'
import defaultSettings from '@/settings'
import jnpf from '@/utils/jnpf'

const {
  // ...
  fontSizeClass
} = defaultSettings

const state = {
  // ...
  fontSizeClass: jnpf.storageGet('fontSizeClass') === null ? fontSizeClass : jnpf.storageGet('fontSizeClass')
}

const mutations = {
  CHANGE_SETTING: (state, { key, value }) => {
    if (state.hasOwnProperty(key)) {
      state[key] = value
      jnpf.storageSet({
        [key]: value
      })
    }
  }
}

const actions = {
  changeSetting({ commit }, data) {
    commit('CHANGE_SETTING', data)
  }
}

export default {
  namespaced: true,
  state,
  mutations,
  actions
}
```



### 使用者切換設定

src/layout/components/settings/index.vue

```vue
<div class="fontList">
  <el-tooltip class="item" effect="dark" :content="$t(`settings.${item4.className}`)"
              placement="top" v-for="(item4,index4) in fontSizeCssConfig" :key="index4">
    <el-tag @click="checkFont(item4)">
      {{ item4.className }}
      <i class="el-icon-check bg-color-2" v-if="item4.className===fontSizeClass"></i>
    </el-tag>
  </el-tooltip>
</div>
```

```js
import fontSizeCongif from '@/assets/scss/fontSize.scss'
export default {
  data() {
    return {
      fontSizeClass: '',
      fontSizeCssConfig: [
        {
          name: '大',
          className: 'large',
          fontSize: fontSizeCongif.large
        },
        {
          name: '中',
          className: 'medium',
          fontSize: fontSizeCongif.medium
        },
        {
          name: '小',
          className: 'small',
          fontSize: fontSizeCongif.small
        },
        {
          name: '迷你',
          className: 'mini',
          fontSize: fontSizeCongif.mini
        },
      ],
    }
  },
  computed: {
    // 寫進store
    defaultFontSizeClass() {
      return this.$store.state.settings.fontSizeClass
    },
  },
  watch: {
    defaultFontSizeClass: {
      handler: function (val, oldVal) {
        if (!val) return
        this.fontSizeClass = val
        let activeItem = this.fontSizeCssConfig.filter(o => o.className === val)[0]
        this.font = activeItem && activeItem.fontSize ? activeItem.fontSize : "12px"
      },
      immediate: true
    },
  },
  methods: {
    checkFont(item) {
      if (item.className === this.fontSizeClass) return
      this.fontSize = item.className
      this.$store.dispatch("settings/changeSetting", {
        key: "fontSizeClass",
        value: item.className
      })
    }
  }
}
```



### 套用至 Layout

src/layout/plain/index.vue

src/layout/functional/index.vue

src/layout/classic/index.vue

```vue
<div :class="classObj" class="app-wrapper classic">
  <!--...-->
</div>
```

```js
export default {
  computed: {
    ...mapState({
      // ...
      fontSizeClass: state => state.settings.fontSizeClass
    }),
    classObj() {
      return {
        // ...
        [this.fontSizeClass]: true
      };
    }
  },
}
```

src/layout/plain/sidebar/index.vue

src/layout/plain/sidebar/SidebarItem.vue

src/layout/functional/menu/SidebarItem.vue

src/layout/classic/sidebar/SidebarItem.vue

```vue
<el-submenu otherAttributes='...'
            :popper-class="`${slideClass} ${themeClass} ${layoutType} ${fontSizeClass}`">
	<!--...-->
</el-submenu>
```

```js
export default {
  computed: {
    ...mapState({
      //...
      fontSizeClass: state => state.settings.fontSizeClass,
    }),
  }
}
```



