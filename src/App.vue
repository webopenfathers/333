<template>
  <div id="app">
    <div :class="{ mark: markB }">
      <div class="content" id="js-mark-content-id" v-if="content"></div>
      <div class="tooltip-box" id="js-tooltip-box-id" v-if="toolTip">
        <!-- {{ content }}

        <button @click="maskFn">退出遮罩</button> -->
        <!-- <button @click="activeFn">切换</button> -->
        <hello-world
          @changeActive="changeActive"
          @cancelFn="cancelFn"
          :active="active"
        ></hello-world>
      </div>
    </div>
    <div class="list-box">
      <div
        v-for="(item, index) in textArr"
        class="list-box-item"
        :class="{ 'js-show-id': active === index }"
        :key="index"
      >
        {{ item }}
      </div>
      <button @click="element" class="btn">元素</button>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
export default {
  components: { HelloWorld },
  name: "App",
  // components: {},
  data() {
    return {
      //
      markB: true,
      toolTip: true,
      content: true,
      //
      contentMark: null,
      showClone: null,
      active: 0,
      textArr: [
        "花自飘零bnnnnnnnnnnnnnnnnnn水自流",
        "一种相思",
        "两处闲愁",
        "此情无计可消除",
        "才下眉头",
        "却上心头",
      ],
    };
  },
  mounted() {
    console.log(666);
    this.fn();
  },
  methods: {
    element() {
      console.log("我被点击了");
    },
    cancelFn() {
      this.markB = false;
      this.toolTip = false;
      this.content = false;
    },
    maskFn() {
      this.markB = !this.markB;
    },
    changeActive() {
      this.contentMark.removeChild(this.showClone);
      this.fn();
    },
    fn() {
      let show = null;
      if (this.active <= 5) {
        show = document.querySelector(".js-show-id");
      } else {
        show = document.querySelector(".btn");
      }
      this.active == 6 ? (this.active = 0) : (this.active += 1);
      // 获取到当前要显示的元素
      const showLeft = show.offsetLeft;
      console.log(showLeft);
      const showTop = show.offsetTop;
      // const showWidth = show.offsetWidth;
      const showHeight = show.offsetHeight;
      //设置一个框
      const contentMark = document.getElementById("js-mark-content-id");
      contentMark.style.left = showLeft - 3 + "px";
      contentMark.style.top = showTop - 3 + "px";
      const showClone = show.cloneNode(show);
      this.showClone = showClone;
      this.contentMark = contentMark;
      contentMark.appendChild(showClone);

      //设置一个提示语
      const tooltipBox = document.getElementById("js-tooltip-box-id");
      tooltipBox.style.left = showLeft + "px";
      tooltipBox.style.top = showTop + showHeight + 15 + "px";
    },
  },
};
</script>

<style>
/* 高亮元素盒子 */
.list-box {
  margin-top: 60px;
}

/* 高亮元素样式 */
.list-box-item {
  list-style: none;
  background: paleturquoise;
  float: left;
  margin: 2px;
  padding: 5px;
}

/* 遮罩层 */
.mark {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  overflow: hidden;
  outline: 0;
  -webkit-overflow-scrolling: touch;
  background-color: rgb(0, 0, 0);
  filter: alpha(opacity=60);
  background-color: rgba(0, 0, 0, 0.3);
  z-index: 521;
}

/* 高亮区域 */
.content {
  z-index: 1314;
  border: 1px dashed #fff;
  position: absolute;
}

/* 有意见，把肚子里的吐?出来 */
.tooltip-box {
  /* height: 26px; */
  /* line-height: 26px; */
  display: inline-block;
  /* background: white; */
  position: relative;
  /* -moz-border-radius: 40px;
  -webkit-border-radius: 40px;
  border-radius: 40px; */
  padding: 2px 15px;
  /* font-size: 14px; */
}

/*加个小尾巴*/
.tooltip-box:before {
  content: "";
  position: absolute;
  right: 100%;
  top: -10px;
  left: 3%;
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  border-bottom: 13px solid white;
}
</style>