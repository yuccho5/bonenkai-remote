<template>
  <div class="animation-container">
    <!--<img class="background" src="@/assets/sky-background.png"> -->
    <img class="lower-jaw" :class="{ 'dinosaur-jaw-open': isJawOpen }" src="@/assets/dinosaur-lower-jaw.png">
    <img class="non-mouth" src="@\assets\dinosaur-non-mouth.png">
    <img class="egg" v-show="isEggVisible" :class="{ 'egg-visible': isEggRotating }"  src="@/assets/egg.png">  
  </div>
</template>

<script>
import anime from 'animejs';

export default {
  data() {
    return {
      isJawOpen: false,
      isEggVisible: false, // 卵が見えるかどうか
     // isEggRotating: false,  卵が回転するかどうか
    };
  },
  mounted() {
       // 少し時間を置いてから口を開く
    setTimeout(() => {
      this.openJaw();
      setTimeout(() => {
        this.showEgg();
      }, 500); // 口が開いてから500ミリ秒後に卵を表示
    }, 200); // 200ミリ秒後に口を開く
  },

  methods: {
    openJaw() {
      // 口を開く処理
      this.isJawOpen = true;
    },
    showEgg() {
      this.isEggVisible = true;
      this.startEggAnimation();
    },
    startEggAnimation() {
      anime({
        targets: '.egg',
        translateX:[ 
         { value: -360, duration: 1500, easing: 'easeInOutQuad' } //  
        ],
        translateY: [
         { value: -50, duration: 700, easing: 'easeInOutQuad' },
         { value: 200, duration: 800, easing: 'easeInOutQuad' }, // 最初に上に飛び出す
         { value: 170, duration: 300, easing: 'easeOutCubic' },
         { value: 200, duration: 150, easing: 'linear' }
        ],
        scale: [
         { value: 1.5, duration: 500, easing: 'linear' },
         { value: 3, duration: 1000, easing: 'linear' }     // 元のサイズに戻る
        ],
       
        /*rotate: {
          value: 360,
          duration: 2000,
          easing: 'linear'  均一な速さで回転
       },*/
        duration: 1500 
     });
    }
  }
};

</script>

<style scoped>
.animation-container {
  position: relative;
  width: 100vw; /* コンテナの幅をビューポート幅に設定 */
  height: 100vh; /* コンテナの高さをビューポート高さに設定 */
  overflow: hidden; /* コンテナ外の要素を非表示にする */
}
.non-mouth {
  position: absolute;
  width: 50vw; /* 画像のサイズを調整 */
}

.lower-jaw {
  position: absolute;
  right: 15.3vw; /* 画面幅の20%分右から離れる */
  bottom: 48.5vh; /* 画面高さの10%分下から離れる */
  width: 41.8vw; /* 画像のサイズを調整 */
  z-index: 1; /* 下口の画像を前面に表示 */
  transform-origin: 60% 40%; 
  /*transition: transform 1.0s ease;  アニメーションの速度とイージング */
}

/* アニメーションがアクティブな状態 */
.dinosaur-jaw-open {
  transform: rotate(-35deg); /* 反時計回りに30度回転 */
}

.egg {
  position: absolute;
  width: 13vw; /* 卵の画像の幅をビューポート幅の10%に設定 */
  right: 35vw; /* 画面幅の20%分右から離れる */
  bottom: 58vh; /* 画面高さの10%分下から離れる */
  opacity: 1; /* 初期状態では見えない */
  z-index: 10; /* 他の要素よりも前面に表示 */
  /* transition:transform 2s;  透明度と変形のアニメーション設定 */
}

@media (max-width: 600px) {
  .non-mouth, .lower-jaw {
    width: 70vw; /* スマートフォン表示で画像の幅を変更 */
  }
  .egg {
    width: 15vw; /* スマートフォン表示で卵の画像の幅を変更 */
  }
}
</style>