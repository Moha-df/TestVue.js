<template>
  <div id="app">
    <MyCanvas ref="myCanvas" />
    <CanvasLogic ref="canvasLogic" />
    <CanvasPanel />
  </div>
</template>

<script>
import MyCanvas from './components/MyCanvas.vue';
import CanvasLogic from './components/CanvasLogic.vue';
import CanvasPanel from './components/CanvasPanel.vue';

export default {
  name: 'App',
  components: {
    MyCanvas,
    CanvasLogic,
    CanvasPanel,
  },
};
</script>