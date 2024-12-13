<template>
  <div>
    <button @click="triggerDrawCircle">Dessiner un cercle</button>
    <button @click="triggerErasePanel">Effacer le panneau</button>
    <button @click="triggerDrawSquare">Dessiner un carré</button>
    <button @click="triggerZoomIn">Zoomer</button>
    <button @click="triggerZoomOut">Dézoomer</button>
    <p>{{ lastAction }}</p>
  </div>
</template>

<script>
export default {
  name: 'PanelCanvas',
  props: {
    logicCanvasData: Object
  },
  computed: {
    lastAction() {
      if (this.logicCanvasData) {
        return `Dernière action : ${this.logicCanvasData.action}`;
      }
      return 'Aucune action effectuée';
    }
  },
  methods: {
    triggerDrawCircle() {
      this.$emit('action', 'drawCircle');
    },
    triggerErasePanel() {
      this.$emit('action', 'erasePanel');
    },
    triggerDrawSquare() {
      this.$emit('action', 'drawSquare');
    },
    triggerZoomIn() {
      this.$emit('action', 'zoomIn');
    },
    triggerZoomOut() {
      this.$emit('action', 'zoomOut');
    }
  }
}
</script>