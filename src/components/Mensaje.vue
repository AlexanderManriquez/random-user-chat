<template>
    <div
      class="burbuja-mensaje"
      :class="{ 'mensaje-derecha': isSender }"
      :style="{ backgroundColor: color }"
    >
      <p><strong>{{ sender }}:</strong></p>
      <p>{{ text }}</p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      text: {
        type: String,
        required: true,
      },
      sender: {
        type: String,
        required: true,
      },
      color: {
        type: String,
        required: true,
      },
      isSender: {
        type: Boolean,
        default: false, // Indica si el mensaje es del usuario local
      },
    },
  };
  </script>
  
  <style scoped>
  .burbuja-mensaje {
    max-width: 60%;
    padding: 10px;
    border-radius: 10px;
    margin: 10px;
    color: #fff;
    text-align: left;
  }
  
  .mensaje-derecha {
    align-self: flex-end;
    border-top-right-radius: 0;
  }
  
  .burbuja-mensaje:not(.mensaje-derecha) {
    align-self: flex-start;
    border-top-left-radius: 0;
  }
  </style>
  