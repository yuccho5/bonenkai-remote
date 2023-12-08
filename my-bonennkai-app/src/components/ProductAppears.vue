<template>
  <div class="product-container" @click="notifyParent">
    <div class="product-background"></div>
    <img class="product-image" src="@/assets/kei_SR.png"> <!-- 商品画像のパスを指定 -->
    <div class="sparkle-effect"></div>
  </div>
</template>

<script>
export default {
  methods: {
    notifyParent() {
      // 親コンポーネントに通知
      this.$emit('click-on-product');
    }
  }
};
</script>

<style scoped>
.product-container {
  position: relative;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.5); /* 背景を暗くする */
}

.product-image {
  z-index: 2; /* 背景より前面に表示 */
  max-width: 80%; /* 画像の最大幅を設定 */
  max-height: 80%; /* 画像の最大高さを設定 */
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.8); /* 光る影を追加 */
  opacity: 0; /* 初期状態では不透明 */
  transform: translateY(-100px); /* 初期状態では下に少しオフセット */
  animation: fadeInUp 2.0s ease forwards; /* フェードインと上への移動 */
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}  

.sparkle-effect {
  position: absolute;
  width: 100%;
  height: 100%;
  background: none;
  pointer-events: none;
  animation: sparkle 2s infinite; /* キラキラ効果のアニメーションを追加 */
}

/* キラキラ効果のアニメーション */
@keyframes sparkle {
  0%, 100% {
    background: rgba(255, 255, 255, 0);
  }
  50% {
    background: rgba(255, 255, 255, 0.3);
  }
}
</style>
