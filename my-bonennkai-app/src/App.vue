<template>
  <div>
    <DinosaurAnimation v-if="currentStep === 1" @start="handleStart" />
    <DinosaurOpensMouth v-if="currentStep === 2" />
    <EggRollsAndGlows v-if="currentStep === 3" />
    <ProductAppears v-if="currentStep === 4" />
  </div>
</template>

<script>
import DinosaurAnimation from './components/DinosaurAnimation.vue';
import DinosaurOpensMouth from './components/DinosaurOpensMouth.vue';
import EggRollsAndGlows from './components/EggRollsAndGlows.vue';
import ProductAppears from './components/ProductAppears.vue';

export default {
  name: 'App',
  components: {
    DinosaurAnimation,
    DinosaurOpensMouth,
    EggRollsAndGlows,
    ProductAppears
  },
  data() {
    return {
      currentStep: 1 // 現在のステップを追加
    };
  },
  methods: {
    // スタートハンドルの実装
    handleStart() {
      if (this.currentStep < 4) {
        this.currentStep += 1; // 次のステップに進む
     }
    } 
  }     
}
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
