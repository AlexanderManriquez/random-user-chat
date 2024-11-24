<template>
  <div class="chat-display">
    <Mensaje
      v-for="(message, index) in messages"
      :key="index"
      :text="message.text"
      :sender="message.sender"
      :color="message.color"
      :isSender="message.isSender"
    />
  </div>
</template>

<script>
import Mensaje from "./Mensaje.vue";

export default {
  components: { Mensaje },
  props: {
    messages: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.chat-display {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 10px;
  margin-top: 20px;
  max-height: 300px;
  overflow-y: auto;
  background-color: #f9f9f9;
}
</style>
