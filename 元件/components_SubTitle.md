## SubTitle 表單副標題

![image-20210701202037882](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210701202037882.png)

- 使用方式：直接使用`<SubTitle></SubTitle>`標籤

  用`titleText`屬性指定標題（若未傳標題預設文字為"副標題"）

  ```html
  <el-col :span="24">
    <SubTitle titleText="患者資訊">
      <!-- 插槽 -->
    </SubTitle>
  </el-col>
  ```

  使用範例：

  ```html
  <el-col :span="24">
    <SubTitle titleText="患者資訊">
      <el-col :span="12">
        <el-form-item label="病歷號碼" prop="chartNo">
          <el-input
                    v-model="dataForm.chartNo"
                    placeholder="請輸入"
                    clearable
                    :style="{ width: '100%' }"
                    ></el-input>
        </el-form-item>
      </el-col>
  
      <el-col :span="12">
        <el-form-item label="姓名" prop="patName" required>
          <el-input
                    v-model="dataForm.patName"
                    placeholder="請輸入"
                    clearable
                    :style="{ width: '100%' }"
                    ></el-input>
        </el-form-item>
      </el-col>
    </SubTitle>
  </el-col>
  ```

  

- 其他：可折疊

  ![image-20210701202154254](https://raw.githubusercontent.com/cynthia204z/mybed1/master/img/image-20210701202154254.png)

  預設值為展開，可以透過`:show="false"`使選染完成後預設不展開

  ```html
  <el-col :span="24">
    <SubTitle titleText="患者資訊" :show="false">
      <div>
        <el-col :span="12">
          <el-form-item label="病歷號碼" prop="chartNo">
            <el-input
                      v-model="dataForm.chartNo"
                      placeholder="請輸入"
                      clearable
                      :style="{ width: '100%' }"
                      ></el-input>
          </el-form-item>
        </el-col>
  
        <el-col :span="12">
          <el-form-item label="姓名" prop="patName" required>
            <el-input
                      v-model="dataForm.patName"
                      placeholder="請輸入"
                      clearable
                      :style="{ width: '100%' }"
                      ></el-input>
          </el-form-item>
        </el-col>
      </div>
    </SubTitle>
  </el-col>
  ```

  
