# JNPF Note

## 不顯示在菜單中的分頁

1. 在菜單管理中註冊此頁面，不顯示

2. 開啟新分頁並傳參

   ```js
   // query: 參數
   this.$router.push({ path: '/his7/emr/ierpat/view/IerMainPage', query: { data: object }});
   ```

3. 動態分頁名稱

   ```js
   this.$route.meta.zhTitle = "newName"
   ```

   > 用this.$route.meta.xxxx 讀寫<b style="color:orange">當前頁面</b>的route

4. 取得傳給當前頁的參數

   ```js
   this.$route.query.data
   ```

   

## 刪除當前tag並轉跳前一個路由

```js
let data = {
  path: "/his7/emr/oerpat/view/OerMainPage"
}
this.$router.go(-1);
this.$store.commit('tagsView/DEL_VISITED_VIEW', data)
```



## 從vuex取得用戶資訊

```javascript
import { mapGetters } from 'vuex'

export default {
  computed: {
    ...mapGetters(['userInfo']),
  },
  methods: {
    // 取得
    this.userInfo.userAccount
  }
}
```

```markdown
# 常用
- userId: 用戶id
- userAccount: 用戶帳號
- userName: 用戶姓名

# 其他
- headIcon: 用戶頭像
- departmentId: 部門主鍵
- departmentName: 部門名稱
- organizeId: 組織主鍵
- organizeName: 組織名稱
- positionIds: 崗位
- prevLogin: 上次登錄
- prevLoginTime: 上次登錄時間
- prevLoginIPAddress: 上次登錄IP
- prevLoginIPAddressName: 上次登錄地址
- portalId: 門戶id
```



