# HIS7 NOTE

## 依照科別取得該科醫生

```vue
<el-col :span="6">
  <el-form-item label="科別">
    <el-select v-model="patForm.deptCode" style="width: 100%" @change="deptCodeChange" filterable>
      <el-option
                 v-for="(item, index) in dropDown.deptCodeOptions"
                 :key="index"
                 :value="item.CODE_NO"
                 :label="item.CODE_DESC"
                 ></el-option>
    </el-select>
  </el-form-item>
</el-col>
<el-col :span="6">
  <el-form-item label="主治醫師">
    <el-select v-model="patForm.vsCode" style="width: 100%">
      <el-option
                 v-for="(item, index) in dropDown.docOptions"
                 :key="index"
                 :value="item.CODE_NO"
                 :label="item.CODE_DESC"
                 ></el-option>
    </el-select>
  </el-form-item>
</el-col>
```

```js
import {getDocByDept} from '@/views/his7/emr/utils/dropdow'
export default {
  methods: {
    //科別切換
    deptCodeChange(deptCode){
      this.patForm.vsCode = undefined
      this.searchDeptDoc(deptCode)
    },
    // 查詢該科醫師
    searchDeptDoc(deptCode) {
      getDocByDept(deptCode).then((res)=>{
        this.dropDown.docOptions = res.data
      })
    },
  }
}
```

