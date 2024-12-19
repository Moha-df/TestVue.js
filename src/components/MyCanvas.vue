<template>
  <div ref="canvasContainer" class="canvas-container">
    <canvas ref="canvas" @click="canvasLogcClick" ></canvas>
  </div>
</template>

<script>
export default {
  name: 'MyCanvas',
  mounted() {
    this.initCanvas();
  },
  methods: {
    initCanvas() {
      const canvas = this.$refs.canvas;

      // Set initial canvas size to fill the screen
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;

      const context = canvas.getContext('2d');
      if (context) {
        // Fill the canvas with a gray color
        context.fillStyle = 'gray';
        context.fillRect(0, 0, canvas.width, canvas.height);
      }

      // Listen for window resize events to adjust canvas size
      window.addEventListener('resize', this.handleResize);
    },
    handleResize() {
      const canvas = this.$refs.canvas;
      const tempCanvas = document.createElement('canvas');
      const tempContext = tempCanvas.getContext('2d');

      // Set temporary canvas size to match the original
      tempCanvas.width = canvas.width;
      tempCanvas.height = canvas.height;

      // Copy the current canvas content to the temporary canvas
      tempContext.drawImage(canvas, 0, 0);

      // Update the canvas size to fit the new window dimensions
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;

      const context = canvas.getContext('2d');
      if (context) {

        // Optionally, fill new areas with a background color
        context.fillStyle = 'gray';
        context.fillRect(0, 0, canvas.width, canvas.height);
        // Restore the copied content onto the resized canvas
        context.drawImage(tempCanvas, 0, 0);

      }
    },
    eraseInGray(){
      const canvas = this.$refs.canvas;
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
      const ctx = canvas.getContext('2d');
      ctx.fillStyle = 'gray';
      ctx.fillRect(0, 0, canvas.width, canvas.height);
    },
    drawCircle(x, y, radius, color = 'black') {
      const canvas = this.$refs.canvas;
      const ctx = canvas.getContext('2d');
      ctx.beginPath();
      ctx.arc(x, y, radius, 0, Math.PI * 2);
      ctx.fillStyle = color;
      ctx.fill();
      ctx.closePath();
    },
    canvasLogcClick(e){
      this.$parent.$refs.canvasLogic.isThereAcellHere(e.offsetX, e.offsetY);
    }
  },
  beforeUnmount() {
    // Remove resize event listener when the component is destroyed
    window.removeEventListener('resize', this.handleResize);
  }
};
</script>

<style scoped>
.canvas-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

canvas {
  display: block;
}
</style>
