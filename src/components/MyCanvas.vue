<template>
    <div ref="canvasContainer" class="canvas-container">
      <canvas ref="canvas"></canvas>
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
        
        // Set canvas size to fill the screen
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        
        // Get the canvas rendering context
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
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
  
        const context = canvas.getContext('2d');
        if (context) {
          context.fillStyle = 'gray';
          context.fillRect(0, 0, canvas.width, canvas.height);
        }
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
  