<template>
  <div id="app">
    <MyCanvas ref="myCanvas" />
    <LogicCanvas ref="logicCanvas" @draw="handleDraw" @erase="handleErase" @updateShapes="handleUpdateShapes" @update="handleLogicUpdate" />
    <PanelCanvas :logicCanvasData="logicCanvasData" @action="handleAction" />
  </div>
</template>

<script>
import MyCanvas from './components/MyCanvas.vue';
import LogicCanvas from './components/LogicCanvas.vue';
import PanelCanvas from './components/PanelCanvas.vue';

export default {
  name: 'App',
  components: {
    MyCanvas,
    LogicCanvas,
    PanelCanvas
  },
  data() {
    return {
      logicCanvasData: null
    }
  },
  methods: {
    handleAction(action) {
      this.$refs.logicCanvas[action]();
    },
    handleDraw(shapeData) {
      this.$refs.myCanvas.drawShape(shapeData);
    },
    handleErase() {
      this.$refs.myCanvas.eraseCanvas();
    },
    handleUpdateShapes(shapes) {
      this.$refs.myCanvas.updateShapes(shapes);
    },
    handleLogicUpdate(data) {
      this.logicCanvasData = data;
    },
    startPhysicsUpdate() {
      setInterval(() => {
        if (this.$refs.logicCanvas) {
          this.$refs.logicCanvas.updatePhysics();
        }
      }, 100);
    }
  },
  mounted() {
    setTimeout(() => {
    this.startPhysicsUpdate();
  }, 500);
  }
}
</script>