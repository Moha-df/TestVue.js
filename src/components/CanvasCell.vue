<template>
    <div>
      <!-- No need of visual representation because they are already represented in the canvas -->
    </div>
</template>
  
  <script>
  export default {
    name: 'CanvasCell',
    props: {
      id: {
        type: Number,
        required: true,
      },
      x: {
        type: Number,
        required: true,
      },
      y: {
        type: Number,
        required: true,
      },
      size: {
        type: Number,
        required: true,
      },
    },
    data() {
      return {
        type: 'default',
        content: '',
      };
    },
  };
  </script>