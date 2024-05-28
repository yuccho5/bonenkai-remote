<template>
  <div class="root-container">
      <div class="animation-container">
        <img class="background" src="@/assets/china_red.png">
        <div class="dinosaur-container">
          <img class="lower-jaw" :class="{ 'dinosaur-jaw-open': isJawOpen }" src="@/assets/dinosaur/dinosaur-lower-jaw.png">
          <img class="non-mouth" src="@/assets/dinosaur/dinosaur-non-mouth2.png">
          <img class="egg" v-if="eggImagePath" :src="eggImagePath" :class="{ 'egg-visible': isEggRotating }">
        </div>
        
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
       // 少し時間を置いてから口を開く
    setTimeout(() => {
      this.openJaw();
      setTimeout(() => {
        this.showEgg();        
      }, 200); // 口が開いてから500ミリ秒後に卵を表示
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
      const vm = this;
      const isSmallScreen = window.matchMedia("(max-width: 468px)").matches;

          // 画面幅が468px以下の場合のアニメーション設定
      const smallScreenAnimationSettings = {
        targets: '.egg',
        translateX: [ 
          { value: '-20vw', duration: 2000, easing: 'easeInOutQuad' }
        ],
        translateY: [
          { value: '-10vh', duration: 800, easing: 'easeInOutQuad' },
          { value: '30vh', duration: 1200, easing: 'easeInOutQuad' }
        ],
        scale: [
          { value: 1.5, duration: 400, easing: 'linear' },
          { value: 2, duration: 600, easing: 'linear' },
          { value: 2.5, duration: 800, easing: 'linear' }
        ]
      };


      // 画面幅が468pxより大きい場合のアニメーション設定
      const defaultAnimationSettings = {
        targets: '.egg',
        translateX: [ 
          { value: '-20vw', duration: 1916, easing: 'easeInOutQuad' }
        ],
        translateY: [
          { value: '-10vh', duration: 740, easing: 'easeInOutQuad' },
          { value: '30vh', duration: 1176, easing: 'easeInOutQuad' }
        ],
        scale: [
          { value: 1.5, duration: 400, easing: 'linear' },
          { value: 2, duration: 600, easing: 'linear' },
          { value: 2.5, duration: 800, easing: 'linear' }
         // 元のサイズに戻る
        ]
      };

      // 画面幅に応じて適切なアニメーション設定を選択
      const animationSettings = isSmallScreen ? smallScreenAnimationSettings : defaultAnimationSettings;

       // anime.jsを使用してアニメーションを開始
      anime({
        ...animationSettings,
        complete: function() {
          // キラキラ効果のアニメーションを再生する
          const sparkleEffect = document.querySelector('.sparkle-effect');
          sparkleEffect.style.animationPlayState = 'running';

          // アニメーションが完了したら少し待ってからイベントを発火
          setTimeout(() => {
            vm.$emit('animation-finished');
          }, 300); // 300ミリ秒の遅延
       }
     });
    }
  }
}
        

</script>

<style scoped>
/* CSSリセット */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html, body {
  height: 100%;
  overflow: hidden;
}
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

.dinosaur-container {
  position: absolute;
  right: -5.1%; /* 位置を調整 */
  bottom: 14.4%; /* 位置を調整 */
  width: 56.5vw; /* コンテナの幅をビューポート幅の60%に設定 */
  z-index: 4; /* z-indexを調整 */
}

.non-mouth {
  width: 100%; /* コンテナの幅に合わせる */
  height: auto; /* 高さを自動調整 */
}


.lower-jaw {
  right: 32.0%; /* 位置を調整 */
  bottom: 44.2%; /* 位置を調整 */
  width: 42.5vw; /* コンテナの幅をビューポート幅の60%に設定 */
  position: absolute;
  transform-origin: 60% 40%;
}

/* アニメーションがアクティブな状態 */
.dinosaur-jaw-open {
  transform: rotate(-35deg); /* 反時計回りに30度回転 */
}

.egg {
  position: absolute;
  width: 13vw; /* 卵の画像の幅をビューポート幅の10%に設定 */
  right: 60%; /* 画面幅の20%分右から離れる */
  bottom: 58%; /* 画面高さの10%分下から離れる */
  opacity: 0; /* 初期状態では見えない */
  z-index: 10; /* 他の要素よりも前面に表示 */
  transition: opacity 0.5s ease; /* 卵の透明度の変化にアニメーションを適用 */
}

.egg-visible {
  opacity: 1; /* 卵が見える状態 */
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

@media (max-width: 768px) {
  .dinosaur-container {
    width: 70vw;
    right: -5%;
    bottom: 20%;
  }

  .non-mouth {
    width: 100%;
    bottom: 0;
    right: 0;
  }

  .lower-jaw {
    width: 52vw;
    bottom: 100;
    right: 1000;
  }

  .egg {
    width: 15vw;
  }
}

@media (max-width: 480px) {
  .dinosaur-container {
    width: 100vw;
    right: -10%;
    bottom: 40%;
  }

  .non-mouth {
    width: 100%;
    bottom: 0;
    right: 0;
  }

  .lower-jaw {
    width: 72vw;
    bottom: 100;
    right: 1000;
  }

  .egg {
    width: 25vw;
  }
}
</style>