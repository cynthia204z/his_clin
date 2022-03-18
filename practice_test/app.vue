<template>
  <div>
    <div :style="majorStyle" class="box1 m10">{{text}}</div>

    <input type="file" class="m10" />
    <br />

    <input id="ckb" class="m10" type="checkbox" v-model="checkbox" />
    <label for="ckb">雙色漸層</label>
    <div v-if="checkbox" class="m10">
      <input id="toRight" type="radio" value="toRight" v-model="rotate" />
      <label for="toRight">從左至右</label>
      <input id="toBottom" type="radio" value="toBottom" v-model="rotate" />
      <label for="toBottom">從上至下</label>
      <input id="Deg" type="radio" value="Deg" v-model="rotate" />
      <label for="Deg">自訂角度</label>
      <input
        id="rotateDeg"
        v-if="rotate === 'Deg'"
        v-model="rotateDeg"
        @input="resetGradient"
        style="width:40px;"
        type="number"
        max="999"
        min="-999"
        onKeyDown="if(this.value.length==3) return false;"
      />
      <label for="rotateDeg" v-if="rotate === 'Deg'">°</label>
    </div>
    <div class="m10 colorbox-collection">
      <div
        v-for="(item, index) in imgThemeColorList"
        :key="index"
        class="colorbox"
        :style="getImgThemeColor(index, item)"
        @click="setMajorThemeBG(item)"
      >
        <span
          v-if="checkbox"
        >{{currentColorBox1 === item ? '1' : currentColorBox2 === item ? '2' : ''}}</span>
      </div>
    </div>

    <img ref="myImg" class="preview imgStyle m10" />
    <div>
      <test :text.sync="text" class="m10"></test>
    </div>
  </div>
</template>
<script>
module.exports = {
  name: "index",
  components: {
    test: httpVueLoader("./test.vue"),
  },
  data() {
    return {
      text: "Hello World!",
      majorTheme: {
        color: "#fff",
        background: "gray",
        "font-weight": "bold",
        border: "1px solid #2e2e2e",
      },

      swatches: 19,
      image: undefined,
      input: undefined,
      imgThemeColorList: [],
      currentColorBox1: undefined,
      currentColorBox2: "255, 255, 255",
      currentIndex: 1,

      checkbox: false,
      rotate: "toRight",
      rotateDeg: 45,
    };
  },
  created() {
    this.$nextTick(() => {
      this.image = document.querySelector(".preview");
      this.input = document.querySelector('[type="file"]');

      this.input.onchange = (e) => {
        this.image.src = URL.createObjectURL(this.input.files[0]);
      };

      this.image.onload = () => {
        this.imgThemeColorList = [];
        URL.revokeObjectURL(this.image.src);
        let colors = colorThief.getPalette(this.$refs.myImg, this.swatches);
        function getRGBString(rgb) {
          return `${rgb[0]}, ${rgb[1]}, ${rgb[2]}`;
        }
        function grayLevel(rgbArr) {
          var r = rgbArr[0],
            g = rgbArr[1],
            b = rgbArr[2];
          return r * 0.299 + g * 0.587 + b * 0.114;
        }
        colors = [...new Set(colors)];
        colors.sort((a, b) => {
          return grayLevel(a) - grayLevel(b);
        });
        colors.forEach((c, index) => {
          let rgb = getRGBString(colors[index]);
          this.imgThemeColorList.push(rgb);
        });
      };
    });
  },
  watch: {
    // 漸層角度變化
    rotate() {
      this.resetGradient();
    },
    // 是否開啟漸層
    checkbox(newVal){
      // 重設色票選擇2
      this.currentColorBox2 = "255, 255, 255";
      // 開啟：下一個選擇的色票號碼是2號
      if (newVal) {
        if(this.currentColorBox1){
          this.currentIndex = 2
        }
      }
      // 關閉：設為單色
      else{
        this.setMajorThemeBG(this.currentColorBox1)
      }
    }
  },
  computed: {
    majorStyle() {
      return this.majorTheme;
    },
    "current-colorbox"() {
      return {
        border: "2px solid " + this.majorTheme.background,
      };
    },
  },
  methods: {
    // 色票
    getImgThemeColor(num, item) {
      let rgb = this.imgThemeColorList[num];
      return {
        background: `rgb(${rgb})`,
        border: this.checkIsCurrent(item)
          ? `solid 3px rgb${rgb}`
          : "solid 3px transparent",
        "box-shadow": this.checkIsCurrent(item)
          ? `inset 0 0 0 2px #fff`
          : "none",
      };
    },
    // 判斷是不是當前選擇的色票
    checkIsCurrent(item, num) {
      if (!num) {
        return this.currentColorBox1 === item || this.currentColorBox2 === item;
      } else {
        return this[`currentColorBox${num}`] === item;
      }
    },
    // 根據選擇的色票設定樣式
    setMajorThemeBG(rgb) {
      // 單色
      if (!this.checkbox) {
        this.currentColorBox1 = rgb;
        this.majorTheme.background = `rgb(${rgb})`;
      }
      // 漸層 
      else {
        // 取消漸層色1
        if (this.checkIsCurrent(rgb, 1)) {
          this.currentColorBox1 = "255, 255, 255";
          this.currentIndex = 1;
        }
        // 取消漸層色2
        else if (this.checkIsCurrent(rgb, 2)) {
          this.currentColorBox2 = "255, 255, 255";
          this.currentIndex = 2;
          if (this.checkIsCurrent("255, 255, 255", 1)) {
            this.currentIndex = 1;
          }
        }
        // 新的漸層色
        else {
          this[`currentColorBox${this.currentIndex}`] = rgb;
          this.currentIndex = this.currentIndex === 1 ? 2 : 1;
        }
        // 重設漸層角度
        this.resetGradient();
      }
    },
    // 漸層角度設定
    resetGradient() {
      let rotateType;
      if (this.rotate === "toRight") {
        rotateType = "to right";
      } else if (this.rotate === "toBottom") {
        rotateType = "to bottom";
      } else {
        rotateType = `${this.rotateDeg}deg`;
      }
      this.majorTheme.background = `linear-gradient(${rotateType}, rgb(${this.currentColorBox1}), rgb(${this.currentColorBox2}))`;
    },
  },
};
</script>
<style scoped>
</style>
