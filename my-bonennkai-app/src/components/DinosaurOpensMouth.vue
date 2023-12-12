<template>
  <div class="root-container">
      <div class="animation-container">
        <img class="background" src="@/assets/gold_small.png">
        <img class="lower-jaw" :class="{ 'dinosaur-jaw-open': isJawOpen }" src="@/assets/dinosaur-lower-jaw.png">
        <img class="non-mouth" src="@/assets/dinosaur-non-mouth.png">
        <img class="egg" v-if="eggImagePath" :src="eggImagePath" :class="{ 'egg-visible': isEggRotating }">
     </div>
      <div class="sparkle-effect"></div>
  </div>
</template>

<script>
import anime from 'animejs';

export default {
  props: {
    eggImagePath: String // 卵の画像のパス
  },
  data() {
    return {
      isJawOpen: false,
      isEggVisible: false, // 卵が見えるかどうか
      isEggRotating: false, // 卵が回転するかどうか
    };
  },
  mounted() {
    // Vue コンポーネントの this を保存
    // this.nextEgg(); // 口を開く前に次の卵の色に切り替え

       // 少し時間を置いてから口を開く
    setTimeout(() => {
      this.openJaw();
      setTimeout(() => {
        this.showEgg();        
      }, 600); // 口が開いてから500ミリ秒後に卵を表示
    }, 200); // 200ミリ秒後に口を開く
  },

  methods: {
    openJaw() {      
      // 口を開く処理
      this.isJawOpen = true;
    },
    showEgg() {
      this.isEggVisible = true;
      this.isEggRotating = true;
      this.startEggAnimation();
    },

    startEggAnimation() {
        // eslint-disable-next-line no-unused-vars
      const vm = this;
      anime({
        targets: '.egg',
        translateX:[ 
         { value: -360, duration: 1500, easing: 'easeInOutQuad' } //  
        ],
        translateY: [
         { value: -50, duration: 700, easing: 'easeInOutQuad' },
         { value: 200, duration: 800, easing: 'easeInOutQuad' } // 最初に上に飛び出す
        // { value: 170, duration: 200, easing: 'easeOutCubic' },
        // { value: 200, duration: 150, easing: 'linear' }
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
        duration: 1500,

        complete: function() {
          // キラキラ効果のアニメーションを再生する
          const sparkleEffect = document.querySelector('.sparkle-effect');
          sparkleEffect.style.animationPlayState = 'running';

          // アニメーションが完了したら少し待ってからイベントを発火
          setTimeout(() => {
            vm.$emit('animation-finished');
          }, 300); // 1秒（1000ミリ秒）の遅延
        }
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

.background {
  position: absolute;  /* 画面に固定されるように設定 */
  right: 0; /* 上端から0の位置に設定 */
  bottom: 0; /* 左端から0の位置に設定 */
  width: 100vw; /* 背景画像の幅をビューポート幅に設定 */
  height: 100vh; /* 背景画像の高さをビューポート高さに設定 */
  z-index: 1; /* 背景を他の要素よりも背面に表示 */
}
.non-mouth {
  position: absolute;
  width: 50vw; /* 画像のサイズを調整 */
  z-index: 2;
}

.lower-jaw {
  position: absolute;
  right: 16.0vw; /* 画面幅の20%分右から離れる */
  bottom: 59.0vh; /* 画面高さの10%分下から離れる */
  width: 36.5vw; /* 画像のサイズを調整 */
  z-index: 5; /* 下口の画像を前面に表示 */
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

.sparkle-effect {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(255, 255, 255, 0);
  pointer-events: none;
  animation: sparkle 1.5s ease-out forwards;
  animation-play-state: paused; /* 初期状態ではアニメーションを一時停止 */
  z-index: 20; /* 他の要素よりも上に表示 */
}

@keyframes sparkle {
  0% {
    background: rgba(255, 255, 255, 0);
  }
  50% {
    background: rgba(255, 255, 255, 0.8);
  }
  100% {
    background: rgba(255, 255, 255, 0);
  }
}
</style>