<template>
  <div class="canvas-panel">
    <button class="panel-button" @click="addNewNode">New Node</button>
    <button class="panel-button" @click="eraseCanvas">Erase</button>
    <button class="panel-button" @click="centerCanvas">Center</button>
  </div>
</template>

<script>
export default {
  name: 'CanvasPanel',
  methods: {
    addNewNode() {
      const x = Math.random() * window.innerWidth;
      const y = Math.random() * window.innerHeight;
      this.$parent.$refs.canvasLogic.addCell(x, y);
    },
    eraseCanvas() {
      this.$parent.$refs.canvasLogic.cells = [];
    },
    centerCanvas() {
      this.$parent.$refs.canvasLogic.offsetX = 0;
      this.$parent.$refs.canvasLogic.offsetY = 0;
      this.$parent.$refs.canvasLogic.zoomLevel = 1;
    },
  },
};
</script>
  
  <style scoped>
  .canvas-panel {
    position: fixed;
    bottom: 8%;
    width: 100%;
    display: flex;
    justify-content: center;
    background-color: rgba(0, 0, 0, 0.0);
    padding: 10px 0;
  }
  
  .panel-button {
    color: white;
    background-color: rgba(0, 0, 0, 0.7);
    border: none;
    padding: 10px 20px;
    margin: 0 5px;
    font-size: 16px;
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.3s ease;
  }
  
  .panel-button:hover {
    background-color: rgba(0, 0, 0, 0.9);
  }
  </style>
  