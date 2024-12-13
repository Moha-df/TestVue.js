<template>
  <canvas ref="canvas" width="500" height="500" style="border: 1px solid black;" @wheel="handleWheel" @mousedown="handleMouseDown" @mousemove="handleMouseMove" @mouseup="handleMouseUp"></canvas>
</template>

<script>
export default {
  name: 'MyCanvas',
  data() {
    return {
      dragging: false,
      startX: 0,
      startY: 0,
    };
  },
  mounted() {
    this.initCanvas();
  },
  methods: {
    initCanvas() {
      const canvas = this.$refs.canvas;
      const ctx = canvas.getContext('2d');
      ctx.fillStyle = 'white';
      ctx.fillRect(0, 0, canvas.width, canvas.height);
    },
    drawShape(shape) {
      const canvas = this.$refs.canvas;
      const ctx = canvas.getContext('2d');
      if (shape.type === 'circle') {
        ctx.beginPath();
        ctx.arc(shape.x, shape.y, shape.radius, 0, 2 * Math.PI);
        ctx.fillStyle = shape.color;
        ctx.fill();
        ctx.stroke();
      } else if (shape.type === 'square') {
        ctx.fillStyle = shape.color;
        ctx.fillRect(shape.x, shape.y, shape.size, shape.size);
        ctx.strokeRect(shape.x, shape.y, shape.size, shape.size);
      }
    },
    eraseCanvas() {
      const canvas = this.$refs.canvas;
      const ctx = canvas.getContext('2d');
      ctx.clearRect(0, 0, canvas.width, canvas.height);
    },
    updateShapes(shapes) {
      this.eraseCanvas();
      shapes.forEach(shape => this.drawShape(shape));
    },
    handleWheel(event) {
      event.preventDefault();
      if (event.deltaY < 0) {
        // Scroll up
        this.$parent.$refs.logicCanvas.zoomIn();
      } else {
        // Scroll down
        this.$parent.$refs.logicCanvas.zoomOut();
      }
    },
    handleMouseDown(event) {
      this.dragging = true;
      this.startX = event.clientX;
      this.startY = event.clientY;
    },
    handleMouseMove(event) {
      if (this.dragging) {
        const deltaX = event.clientX - this.startX;
        const deltaY = event.clientY - this.startY;
        this.$parent.$refs.logicCanvas.shapes.forEach(shape => {
          shape.x += deltaX;
          shape.y += deltaY;
        });
        this.startX = event.clientX;
        this.startY = event.clientY;
      }
    },
    handleMouseUp() {
      this.dragging = false;
    }
  }
}
</script>