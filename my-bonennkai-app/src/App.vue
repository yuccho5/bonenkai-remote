<template>
  <div id="app" :class="{ 'fade-out': isFadingOut }">
    <DinosaurAnimation v-if="currentStep === 1" @start="handleStart" />
    <DinosaurOpensMouth v-if="currentStep === 2" @animation-finished="handleAnimationFinished" />
    <ProductAppears v-if="currentStep === 3" @click-on-product="handleProductClick" />
  </div>
</template>

<script>
import DinosaurAnimation from './components/DinosaurAnimation.vue';
import DinosaurOpensMouth from './components/DinosaurOpensMouth.vue';
import ProductAppears from './components/ProductAppears.vue';

export default {
  name: 'App',
  components: {
    DinosaurAnimation,
    DinosaurOpensMouth,
    ProductAppears
  },
  data() {
    return {
      currentStep: 1,
      isFadingOut: false, // フェードアウトの状態
    };
  },
  methods: {
      handleStart() {
      // スタートボタンが押されたらステップ2に進む
      this.currentStep = 2;
      },
      handleAnimationFinished() {
          // アニメーションが完了したらステップ3に進む
        this.isFadingOut = true;
        setTimeout(() => {
          this.isFadingOut = false;
          this.currentStep = 3;
        }, 400); // フェードアウトの持続時間
      },
      handleProductClick() {
      // 商品画像がクリックされたら最初のステップに戻る
      this.currentStep = 1;
      }
   }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
