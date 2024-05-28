<template>
  <div class="animation-container">
    <img class="background" src="@/assets/china_red.png">
    <div class="fixed-container">
      <img class="dinosaur" src="@/assets/dinosaur/dinosaur.png"> 
      <button class="start-button" v-if="!isAnimationStarted" @click="onStartClick">ガチャ</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isAnimationStarted: false,
    };
  },

  methods: {
    onStartClick() {
      this.$emit('start'); // 親コンポーネントに通知
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

.background {
  position: absolute; /* 画面に固定される代わりにコンテナ内で絶対位置を指定 */
  top: 0; /* コンテナの上端から配置 */
  left: 0; /* コンテナの左端から配置 */
  width: 100%; /* コンテナの幅に合わせる */
  height: 100%; /* コンテナの高さに合わせる */
  z-index: 1; /* 背景を他の要素よりも背面に表示 */
}
.fixed-container {
  position: absolute;
  left: 50%;
  bottom: 5%;
  transform: translateX(-50%);
  z-index: 2;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.start-button {  
  color: red; /* ボタンのテキスト色 */
  border: 2px solid black; /* 金色の縁 */
  font-family: 'Sawarabi Mincho', sans-serif; /* Sawarabi Mincho フォントを適用 */
  font-size: 3.2em; /* フォントサイズを現在の2倍に設定 */
  font-weight: bold; /* フォントを太字に設定 */
  text-shadow: 2px 2px 2px rgba(0, 0, 0, 0.8); /* 黒い輪郭を設定 */

  background-color: #FFD700; /* ボタンの背景色 */
  background-image: linear-gradient(to top, #FFD700, #FFFF00); /* グラデーションを追加 */
  border: 2px solid black; /* 枠線 */
  border-radius: 15px; /* 角丸の形状 */
  padding: 12px 24px; /* ボタン内の余白 */
  cursor: pointer; /* マウスオーバー時のカーソルをポインタに */
  transition: background-color 0.3s ease; /* 背景色の変化にトランジションを適用 */
  margin-bottom: 0px;

 /*  position: absolute; /* 絶対位置指定 */
  /* left: 15%; /* 画面の左側からの位置 */
 /*  bottom: 30%; /* 画面の下側からの位置 */
  /* z-index: 3;  背景よりも背面に表示 */

  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.4), inset 0px 0px 5px rgba(255, 255, 255, 0.8); /* 内側と外側に影を追加 */
  animation: hoverEffect 2s ease-in-out infinite; /* アニメーションを適用 */
  writing-mode: horizontal-tb; /* 横書きに強制 */
}

.start-button:hover {
  transform: translateY(-3px); /* ホバー時に少し持ち上げる */
  box-shadow: 7px 7px 12px rgba(0, 0, 0, 0.5), inset 0px 0px 7px rgba(255, 255, 255, 0.9); /* ホバー時に影を強調 */
}

@keyframes hoverEffect {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px); /* 中間点でボタンを少し持ち上げる */
  }
}

.start-button:hover {
  background-color: darkred; /* ホバー時の背景色 */
}
.dinosaur {
  /*position: absolute; */
  /* right: -10%; /* 位置を調整 */
  /* bottom: 15%;  位置を調整 */
  width: 110%; /* 画像のサイズを調整 */
  /* z-index: 3;  背景よりも背面に表示 */
}


/* 画面サイズが大きいときのスタイル */
@media (max-width: 1024px) {
  .fixed-container {
    bottom: 5%;
  }

  .start-button {
    font-size: 2.5em;
    padding: 18px 36px;
    margin-right: 20; /* 縦方向に配置するため右の余白を削除 */
  }

  .dinosaur {
    width: 130%;
  }
}

/* 画面サイズが小さいときのスタイル */
@media (max-width: 768px) {
  .fixed-container {
    bottom: 5%;
  }

  .start-button {
    font-size: 2.0em;
    padding: 20px 40px;
  }

  .dinosaur {
    width: 150%;
  }
}

@media (max-width: 480px) {
  .fixed-container {
    bottom: 20%;
  }

  .start-button {
    font-size: 1.5em;
    padding: 10px 20px;
  }

  .dinosaur {
    width: 250%;
  }
}

</style>

<style>
/* html, body の高さを100%に設定 */
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: hidden; /* 画面全体のスクロールを無効化 */
}
</style>