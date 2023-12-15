<template>
  <div class="animation-container">
    <img class="background" src="@/assets/china_red.png">
    <img class="dinosaur" src="@/assets/dinosaur/dinosaur.png">
    <!-- 確認ダイアログの追加 -->
    <div v-if="showConfirmDialog" class="confirm-dialog">      
      <p class="dialog-text">もう一度回しますか？</p>
      <div class="dialog-buttons">
        <button @click="confirmClose(true)">はい</button>
        <button @click="confirmClose(false)">いいえ</button>
      </div>
    </div>
    
    <div class="product-container" v-if="selectedProduct">
      <div class="product-background"></div>
      <!-- 商品画像のパスを動的にバインド -->
      <img class="product-image" :src="selectedProduct.imagePath" @click="handleProductClick"> <!-- 商品画像のパスを指定 -->
      <!-- 商品説明を動的にバインド -->
      <div class="product-description">{{ selectedProduct.description }}</div>
      <div class="sparkle-effect"></div>
    </div>
  </div>  
  <!-- selectedProduct が存在しない場合、何も表示しない -->
</template>

<script>
export default {
  props: ['selectedProduct'], // 親コンポーネントから渡されるプロパティ
  data() {
    return {
      showConfirmDialog: false, // 確認ダイアログの表示状態
    };
  },      
  methods: {
    // notifyParent() {
    //   // 親コンポーネントに通知
    //   this.$emit('click-on-product');
    // }
    handleProductClick() {
      // 確認ダイアログを表示
      this.showConfirmDialog = true;
    },
    confirmClose(close) {
      // 「はい」が選ばれた場合、親コンポーネントに通知して初期ステップに戻る
      if (close) {
        this.$emit('click-on-product');
      }
      // ダイアログを閉じる
      this.showConfirmDialog = false;
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
  opacity: 0.3; /* 背景画像を暗くする */
}

.dinosaur {
  position: absolute;
  right: -10%; /* 位置を調整 */
  bottom: 15%; /* 位置を調整 */
  width: 65%; /* 画像のサイズを調整 */
  z-index: 2; /* 背景よりも背面に表示 */
  opacity: 0.3; /* 背景画像を暗くする */
}

.product-container {
  overflow: hidden; /* コンテナ内のスクロールを無効化 */
  position: relative;
  width: 100vw;
  height: 100vh;
  display: flex;
  flex-direction: column; /* 子要素を縦方向に配置 */
  justify-content: center;
  align-items: center;
  z-index: 3; /* 背景より前面に表示 */
  background: rgba(0, 0, 0, 0.8); /* コンテナの背景を暗く半透明に */
}

.product-image {
  z-index: 3; /* 背景より前面に表示 */
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
  background-color: transparent; /* 背景色を透明に */
  /*background-image: linear-gradient(to bottom, transparent, black); グラデーションの適用 */
  color: #FFD700; /* フォントカラーを金色 (#FFD700) に設定 */
  /*font-family: 'Sawarabi Mincho', sans-serif; /* Sawarabi Mincho フォントを適用 */
  font-size: 7.0em; /* フォントサイズを現在の2倍に設定 */
  font-weight: bold; /* フォントを太字に設定 */
  text-shadow: 2px 2px 2px rgba(0, 0, 0, 0.8); /* 黒い輪郭を設定 */
  white-space: nowrap; /* テキストを一行に収める */
  overflow: hidden; /* はみ出したテキストを非表示 */

  border: none; /* すべての境界線を削除 */
  padding: 15px 50px; /* 内側の余白を設定 */
  border-radius: 0; /* 角丸を削除 */
  box-shadow: none; /* 影を削除 */
  position: relative; /* 相対位置に設定 */
  top: 0px; /* 位置を下にずらす */
  z-index: 3; /* 背景と画像よりも前面に表示 */
  text-align: center; /* テキストを中央揃えにする */
  margin-top: 0px; /* 画像との間隔 */
  opacity: 0; /* 初期状態では不透明 */
  transform: none;
  animation: fadeInUpDescription 0.7s ease 1.3s forwards; /* 1秒後にアニメーション開始 */
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

.confirm-dialog {
  background-image: url('@/assets/china_red.png'); /* 画像のパスを指定 */
  background-size: cover; /* 画像をコンテナサイズに合わせて拡大/縮小 */
  background-repeat: no-repeat; /* 画像の繰り返しを防止 */
  position: fixed; /* 画面全体に対して固定位置に設定 */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  
  border: 0.1px solid black; /* 金色の縁 */
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
  display: flex;
  flex-direction: column; /* 縦方向のレイアウトに変更 */
  align-items: center; /* 中央揃え */
  justify-content: space-around;
  width: 300px; /* ダイアログの幅 */
  z-index: 1000; /* 他の要素よりも前面に表示 */
}

/* .confirm-dialog p {
  font-size: 1.2em;
  margin: 0 10px 0 0; /* 右側に余白を設定 
} */

.dialog-text {
  font-size: 1.7em;
  color: white; /* フォントカラーを金色 (#FFD700) に設定 */
  font-weight: bold;  /*フォントを太字に設定 */
  text-shadow: 3px 3px 3px rgba(0, 0, 0, 0.8);  /*黒い輪郭を設定 */
  margin-bottom: 20px; /* ボタンとの間隔 */
  text-align: center;
}

.dialog-buttons {
  display: flex;
  justify-content: space-around;
  width: 100%; /* ボタンをダイアログ幅に合わせる */
}

.confirm-dialog button {
  background-color: #FFD700; /* 緑色の背景 */
  color: white; /* ボタンのテキスト色 */
  font-size: 2.0em;
  font-weight: bold; /* フォントを太字に設定 */
  text-shadow: 2px 2px 2px rgba(0, 0, 0, 0.8); /* 黒い輪郭を設定 */
  
  border: 0.1px solid black; /* 金色の縁 */
  box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.4), inset 0px 0px 5px rgba(255, 255, 255, 0.8); /* 内側と外側に影を追加 */
  padding: 10px 20px;
  text-align: center;
  text-decoration: none;
  display: flex; /* ボタンをフレックスアイテムとして扱う */
  justify-content: center; /* 中央揃え */
  align-items: center; /* 中央揃え */
  flex-grow: 1; /* フレックスコンテナ内で均等に伸ばす */
  flex-basis: 0; /* ボタンの基本的なサイズを0に設定 */
  display: inline-block;
  margin: 4px;
  border-radius: 5px;
  cursor: pointer;
}

.confirm-dialog button:hover {
  transform: translateY(-3px); /* ホバー時に少し持ち上げる */
  box-shadow: 7px 7px 12px rgba(0, 0, 0, 0.5), inset 0px 0px 7px rgba(255, 255, 255, 0.9); /* ホバー時に影を強調 */
}

.confirm-dialog button:nth-child(2) {
  background-color: rgba(204, 0, 0, ); /* 赤色の背景 */
}
</style>
