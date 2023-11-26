<template>
  <div class="animation-container">
    <img class="background" src="@/assets/sky-background.png">
    <img class="dinosaur" src="@/assets/dinosaur.png">
    <img class="lower-jaw" v-show="isMouthOpen" src="@/assets/dinosaur-lower-jaw.png">
    <img class="egg" v-show="isEggVisible" :style="eggStyle" src="@/assets/egg.png">
    <img class="product" v-show="isProductVisible" src="@/assets/product.png">
    <button v-if="!isAnimationStarted" @click="startAnimation">Start</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isMouthOpen: false,
      isEggVisible: false,
      eggStyle: { top: 'initial position' }, // 初期位置
      isProductVisible: false,
      isAnimationStarted: false,
    };
  },
  methods: {
    startAnimation() {
      this.isAnimationStarted = true;
      this.isMouthOpen = true;
      setTimeout(() => {
        this.isEggVisible = true;
        this.eggStyle.top = 'falling position'; // 卵が落ちるアニメーション
        setTimeout(() => {
          this.isProductVisible = true; // 商品画像の表示
        }, 3000); // 卵が落ちてから商品画像が表示されるまでの時間
      }, 2000); // 口が開いてから卵が表示されるまでの時間
    },
    resetAnimation() {
      // アニメーションをリセットするメソッド
    }
  }
};
</script>

<style scoped>
.animation-container {
  position: relative;
}
.background, .dinosaur, .lower-jaw, .egg, .product {
  position: absolute;
}
/* 他のCSSスタイル */
</style>
