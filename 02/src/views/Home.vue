<template>
  <div class="container">
    <div
      class="panel"
      :style="{'--height': height}"
      v-touch:start="startHandler"
      v-touch:end="endHandler"
      v-touch:moving="moveHandler"
    >
      <div class="dot"></div>
      <div class="content-panel">
        <div class="card"></div>
        <div class="card"></div>
        <div class="card"></div>
        <div class="card"></div>
        <div class="card"></div>
        <div class="card"></div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      originY: null,
      offsetTop: null,
      offsetHeight: null,
      height: '400px'
    };
  },
  methods: {
    startHandler(e) {
      this.originY = e.changedTouches[0].clientY;
      this.offsetTop = e.changedTouches[0].target.offsetTop;
      this.offsetHeight = e.changedTouches[0].target.offsetHeight;
      console.log('startHandler -> e', e);
    },
    endHandler(e) {
      console.log('endHandler -> e', e);
    },
    moveHandler(e) {
      const curY= e.changedTouches[0].clientY;
      this.height = `${this.offsetHeight + (this.offsetTop - curY)}px`;
    },
  }
};
</script>
<style lang="scss" scoped>
.container {
  width: 100%;
  height: 100%;
  background: rgb(180, 189, 191);

  .top {
    width: 100%;
    height: 200px;
    background: red;
  }

  .panel {
    position: fixed;
    top: calc(100% - var(--height));
    width: 100%;
    min-height: var(--height);
    background: white;
    border-radius: 20px 20px 0 0;
    cursor: pointer;

    .content-panel {
      width: 100%;
      height: calc(var(--height) - 40px);
      margin-top: 40px;
      display: flex;
      flex-direction: column;
      align-items: center;
      overflow: scroll;
      cursor: pointer;
      .card {
        margin-bottom: 10px;
        min-height: 100px;
        width: 80%;
        background: rgb(105, 177, 105);
      }
    }
    .dot {
      width: 32px;
      height: 4px;
      background: rgba(0, 0, 0, 0.4);
      border-radius: 2px;
      position: absolute;
      top: 10px;
      left: calc(50% - 16px);
      z-index: 10;
    }
  }
}
</style>