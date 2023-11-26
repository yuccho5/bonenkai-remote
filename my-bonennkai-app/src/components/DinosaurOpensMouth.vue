<template>
  <div class="animation-container">
    <!--<img class="background" src="@/assets/sky-background.png"> -->
    <!-- <img class="dinosaur" src="@/assets/dinosaur.png"> -->
    <img class="lower-jaw" src="@/assets/dinosaur-lower-jaw.png">
    <img class="egg" v-show="isEggVisible" :style="eggStyle" src="@/assets/egg.png">  
  </div>
</template>

<script>
export default {
  data() {
    return {
      isEggVisible: false,
      eggStyle: { top: 'initial position' }, // 初期位置
      isProductVisible: false,
      isAnimationStarted: false,
    };
  },
  methods: {
    startAnimation() {
      this.isAnimationStarted = true;
      setTimeout(() => {
        this.isEggVisible = true;
        this.eggStyle.top = 'falling position'; // 卵が落ちるアニメーション
        setTimeout(() => {
          this.isProductVisible = true; // 商品画像の表示
        }, 2000); // 卵が落ちてから商品画像が表示されるまでの時間
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
  width: 100%; /* コンテナの幅を指定 */
  height: 100vh; /* コンテナの高さを指定 */
  overflow: hidden; /* コンテナ外の要素を非表示にする */
}

.dinosaur {
  position: absolute;
  right: 15%; /* 位置を調整 */
  bottom: 15%; /* 位置を調整 */
  width: 60%; /* 画像のサイズを調整 */
}
.lower-jaw {
  position: absolute;
  right: 20%; /* 位置を調整 */
  bottom: 60%; /* 位置を調整 */
  width: 60%; /* 画像のサイズを調整 */
  transform: translateY(100%); /* 口を適切に位置させる */
}
.egg {
  position: absolute;
  right: 20%; /* 位置を調整 */
  bottom: 20%; /* 位置を調整 */
  width: 10%; /* 画像のサイズを調整 */
}
</style>