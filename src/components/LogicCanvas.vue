<script>
export default {
  name: 'LogicCanvas',
  data() {
    return {
      shapes: [],
      scaleFactor: 1,
    }
  },
  methods: {
    drawCircle() {
      const circleData = { type: 'circle', x: 250, y: 250, radius: 50, color: 'blue' };
      this.shapes.push(circleData);
      this.$emit('draw', circleData);
      this.$emit('update', { action: 'Cercle dessiné' });
    },
    drawSquare() {
      const squareData = { type: 'square', x: 200, y: 200, size: 100, color: 'red' };
      this.shapes.push(squareData);
      this.$emit('draw', squareData);
      this.$emit('update', { action: 'Carré dessiné' });
    },
    erasePanel() {
      this.shapes = [];
      this.$emit('erase');
      this.$emit('update', { action: 'Panneau effacé' });
    },
    updatePhysics() {
      this.shapes.forEach(shape => {
        if (shape.type === 'circle') {
          // Logic des circles
        }
        if (shape.type === 'square') {
          // Logic des squares
        }
      });
      this.$emit('updateShapes', this.shapes);
    },
    zoomIn() {
      this.scaleFactor *= 1.1; // Augmenter le facteur de zoom

      this.shapes.forEach(shape => {
        if (shape.type === 'circle') {
          shape.x = shape.x * 1.1;
          shape.y = shape.y * 1.1;
          shape.radius = shape.radius * 1.1;
        } else if (shape.type === 'square') {
          shape.x = shape.x * 1.1;
          shape.y = shape.y * 1.1;
          shape.size = shape.size * 1.1;
        }
      });

      this.$emit('update', { action: 'Zoom in' });
      const shapesCopy = [...this.shapes]; // Create a copy of the shapes array
      this.$emit('updateShapes', shapesCopy); // Emit the updateShapes event with the copy
    },
    zoomOut() {
      this.scaleFactor /= 1.1; // Diminuer le facteur de zoom

      this.shapes.forEach(shape => {
        if (shape.type === 'circle') {
          shape.x = shape.x / 1.1;
          shape.y = shape.y / 1.1;
          shape.radius = shape.radius / 1.1;
        } else if (shape.type === 'square') {
          shape.x = shape.x / 1.1;
          shape.y = shape.y / 1.1;
          shape.size = shape.size / 1.1;
        }
      });

      this.$emit('update', { action: 'Zoom out' });
      const shapesCopy = [...this.shapes]; // Create a copy of the shapes array
      this.$emit('updateShapes', shapesCopy); // Emit the updateShapes event with the copy
    },
  }
}
</script>