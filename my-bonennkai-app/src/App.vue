<template>
  <div id="app" :class="{ 'fade-out': isFadingOut }">
    <DinosaurAnimation v-if="currentStep === 1" @start="handleStart" />
    <DinosaurOpensMouth v-if="currentStep === 2" 
                        :eggImagePath="selectedItem ? selectedItem.eggImagePath : null"
                        @animation-finished="handleAnimationFinished" />
                         <!-- @changeEgg="handleChangeEgg" -->
    <ProductAppears v-if="currentStep === 3" 
                    :selectedProduct="selectedProduct"
                    @click-on-product="handleProductClick" />
  </div>
</template>

<script>
import DinosaurAnimation from './components/DinosaurAnimation.vue';
import DinosaurOpensMouth from './components/DinosaurOpensMouth.vue';
import ProductAppears from './components/ProductAppears.vue';
import itemsData from '@/assets/keihin_list.json';

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
      items: itemsData, // 統合されたデータ
      selectedItemId: null, // 選択されたアイテムのID
      selectedItem: null, // 選択されたアイテム
      selectedProduct: null, // 選択された商品の初期値を null に設定
      selectedEggImagePath: null, // 初期値は null
      currentItemId: 1, // 現在のアイテムID
    };
  },

  created() {
    // JSONファイルから読み込んだデータで画像パスを解決
    this.items = itemsData.map(item => {
      return {
        ...item,
        eggImagePath: require(`@/assets/${item.eggColor}`),
        imagePath: require(`@/assets/${item.imagePath}`)
      };
    });
    console.log(this.items); // これでitemsの内容をコンソールに出力
    // コンポーネントが作成されたときに最初のアイテムを選択
    this.selectItem(1);
  },

  computed: {
    currentEggImage() {
    // 選択されたアイテムから直接卵の画像のパスを取得
    const eggImage = this.selectedItem ? this.selectedItem.eggColor : null;
    console.log('CurrentEggImage:', eggImage);  // 卵の画像パスをログに表示
    return eggImage;
    },

    currentProductImage() {
      // 選択されたアイテムに基づく商品画像を返す
      const item = this.items.find(item => item.id === this.selectedItemId);
      return item ? item.imagePath : null;
    },

    currentProductDescription() {
      // 選択されたアイテムに基づく商品説明を返す
      const item = this.items.find(item => item.id === this.selectedItemId);
      return item ? item.description : null;
    }    
  },    

  methods: {
      selectItem(itemId) {
        // 指定されたIDに基づいてアイテムを選択
        this.selectedItemId = itemId;
        this.selectedItem = this.items.find(item => item.id === itemId);
        this.selectedProduct = this.selectedItem; // ここで selectedProduct を更新
        // 選択されたアイテムをコンソールに出力
        console.log(this.selectedItem);
        console.log('SelectedProduct:', this.selectedProduct);
      },
      

      handleStart() {
        // アニメーション開始時に次のアイテムIDを更新し、選択
        this.currentItemId = (this.currentItemId % this.items.length) + 1;
        this.selectItem(this.currentItemId);
        // ステップ2に進む
        this.currentStep = 2;
      },

      // handleChangeEgg() {
      // // 現在のアイテムIDを次のIDに更新
      // this.currentItemId = (this.currentItemId % 4) + 1;
      // // 更新されたIDに基づいてアイテムを選択
      // this.selectItem(this.currentItemId);
      // },

      handleAnimationFinished() {
        // アニメーション完了時の処理
        if (this.currentStep === 2) {
          this.handleProceedToNextStep();
        }      
      },
      
      handleProceedToNextStep() {
        // ステップ3に進む処理                        
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

   /* スクロールを無効にするスタイル*/
  margin: 0;
  padding: 0; 
  overflow: hidden;
  height: 100vh; /* ビューポートの高さに合わせる*/
  width: 100vw; /* ビューポートの幅に合わせる */
}
</style>
