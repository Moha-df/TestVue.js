<template>
  <div id="app">
    <MyCanvas />
    <CanvasPanel />
  </div>
</template>

<script>
import MyCanvas from './components/MyCanvas.vue';
import CanvasPanel from './components/CanvasPanel.vue';

export default {
  name: 'App',
  components: {
    MyCanvas,
    CanvasPanel
  }
};
</script>
