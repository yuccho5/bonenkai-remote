<template>
  <div class="product-container" @click="notifyParent" v-if="selectedProduct">
    <div class="product-background"></div>
    <!-- 商品画像のパスを動的にバインド -->
    <img class="product-image" :src="selectedProduct.imagePath"> <!-- 商品画像のパスを指定 -->
    <!-- 商品説明を動的にバインド -->
    <div class="product-description">{{ selectedProduct.description }}</div>
    <div class="sparkle-effect"></div>
  </div>
  <!-- selectedProduct が存在しない場合、何も表示しない -->
</template>

<script>
export default {
  props: ['selectedProduct'], // 親コンポーネントから渡されるプロパティ
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
  overflow: hidden; /* コンテナ内のスクロールを無効化 */
  position: relative;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column; /* 子要素を縦方向に配置 */
  justify-content: center;
  align-items: center;
  background: rgba(0, 0, 0, 0.5); /* 背景を暗くする */
}

.product-image {
  z-index: 2; /* 背景より前面に表示 */
  max-width: 70%; /* 画像の最大幅を設定 */
  max-height: 70%; /* 画像の最大高さを設定 */
  box-shadow: 0 0 10px rgba(255, 255, 255, 0.8); /* 光る影を追加 */
  opacity: 0; /* 初期状態では不透明 */
  transform: translateY(-100px); /* 初期状態では下に少しオフセット */
  animation: fadeInUp 2.0s ease forwards; /* 画像のアニメーションは変更せず */
}

@keyframes fadeInUp {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}  

.product-description {
  background-color: white; /* 背景色を白に設定 */
  padding: 50px 140px; /* 内側の余白を設定 */
  border-radius: 10px; /* 角を丸くする */
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.3); /* 影を追加 */
  position: relative; /* 相対位置に設定 */
  top: 0px; /* 位置を下にずらす */
  z-index: 3; /* 背景と画像よりも前面に表示 */
  text-align: center; /* テキストを中央揃えにする */
  color: black; /* テキストの色を黒に設定 */
  margin-top: 25px; /* 画像との間隔 */
  font-size: 1.2em; /* フォントサイズ */
  opacity: 0; /* 初期状態では不透明 */
  transform: translateY(100px); /* 初期状態では下に少しオフセット */
  animation: fadeInUpDescription 2.0s ease 0.5s forwards; /* 1秒後にアニメーション開始 */
}

@keyframes fadeInUpDescription {
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
