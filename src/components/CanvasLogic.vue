<template>
    <div>
      <CanvasCell
        v-for="cell in cells"
        :key="cell.id"
        :id="cell.id"
        :x="cell.x"
        :y="cell.y"
        :size="cell.size"
      />
    </div>
  </template>
  
  <script>
  import CanvasCell from './CanvasCell.vue';
  
  export default {
    name: 'CanvasLogic',
    components: {
      CanvasCell,
    },
    data() {
      return {
        cells: [],
        zoomLevel: 1,
        offsetX: 0,
        offsetY: 0,
      };
    },
    mounted() {
      this.startDrawLoop();
    },
    methods: {
        startDrawLoop() {
        setInterval(() => {
            this.drawCells();
        }, 1000 / 60); // 60 times per second
        },
        drawCells() {
            this.$parent.$refs.myCanvas.eraseInGray();
            // Call MyCanvas to draw all cells
            this.cells.forEach(cell => {
                const drawX = (cell.x + this.offsetX) * this.zoomLevel;
                const drawY = (cell.y + this.offsetY) * this.zoomLevel;
                const size = cell.size * this.zoomLevel;
                this.$parent.$refs.myCanvas.drawCircle(drawX, drawY, size, 'black');
            });
        },
        addCell(x, y) {
            const id = this.cells.length + 1;
            this.cells.push({ id, x, y, size: 50});
        },
        zoomIn() {
            this.zoomLevel *= 1.1;
        },
        zoomOut() {
            this.zoomLevel /= 1.1;  
        },
        moveCanvas(dx, dy) {
            this.offsetX += dx;
            this.offsetY += dy;
        },
        isThereAcellHere(clickX, clickY) {
            for (const cell of this.cells) {
                const drawX = (cell.x + this.offsetX) * this.zoomLevel;
                const drawY = (cell.y + this.offsetY) * this.zoomLevel;
                const radius = cell.size * this.zoomLevel;

                // Calculer la distance entre le clic et le centre du cercle
                const distance = Math.sqrt((clickX - drawX) ** 2 + (clickY - drawY) ** 2);

                if (distance <= radius) {
                    console.log(`Clicked on cell with ID: ${cell.id}`);
                    // Actions supplémentaires si besoin
                    return;
                }
            }

            console.log('Clicked outside of any cells');
        },
    },
  };
  </script>