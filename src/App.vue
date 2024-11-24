<template>
  <div class="app">
    <h1>Chat entre desconocidos</h1>
    <ObtenerUsuario ref="obtenerUsuario" @users-fetched="setUsers" />

    <!-- Diseño de 3 columnas -->
    <div class="chat-layout" v-if="users.length === 2">
      <!-- Panel izquierdo: Usuario 1 -->
      <div class="user-panel">
        <img :src="users[0].picture" alt="Foto de usuario 1" />
        <h3>{{ users[0].name }}</h3>
        <textarea
          v-model="messagesUser1"
          placeholder="Escribe un mensaje..."
        ></textarea>
        <button @click="sendMessage(0)">Enviar</button>
      </div>

      <!-- Columna central: Chat -->
      <Chat :messages="messages" />

      <!-- Panel derecho: Usuario 2 -->
      <div class="user-panel">
        <img :src="users[1].picture" alt="Foto de usuario 2" />
        <h3>{{ users[1].name }}</h3>
        <textarea
          v-model="messagesUser2"
          placeholder="Escribe un mensaje..."
        ></textarea>
        <button @click="sendMessage(1)">Enviar</button>
      </div>
    </div>
  </div>
</template>

<script>
import Chat from "./components/Chat.vue";
import ObtenerUsuario from "./components/ObtenerUsuario.vue";

export default {
  components: { Chat, ObtenerUsuario },
  data() {
    return {
      users: [], 
      messages: [],
      messagesUser1: "",
      messagesUser2: "",
    };
  },
  methods: {
    setUsers(users) {
      this.users = users;
    },
    sendMessage(userIndex) {
      const currentMessage =
        userIndex === 0 ? this.messagesUser1 : this.messagesUser2;

      if (!currentMessage.trim()) return; // Validación de mensajes vacíos

      const newMessage = {
        text: currentMessage,
        sender: this.users[userIndex].name,
        color: this.users[userIndex].color,
        isSender: userIndex === 1,
      };

      this.messages.push(newMessage); // Agregar mensaje al chat

      // Limpiar el input del usuario correspondiente
      if (userIndex === 0) this.messagesUser1 = "";
      if (userIndex === 1) this.messagesUser2 = "";
    },
  },
  mounted() {
    // Llamar al método obtenerUsuario() cuando el componente se monta
    this.$refs.obtenerUsuario.obtenerUsuario();
  },
};
</script>

<style scoped>
/* Estructura general */
.app {
  font-family: Arial, sans-serif;
  max-width: 900px;
  margin: 0 auto;
  text-align: center;
}

.chat-layout {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr; /* 3 columnas */
  gap: 20px;
  margin-top: 20px;
}

.user-panel {
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 20px;
  text-align: center;
}

.user-panel img {
  border-radius: 50%;
  width: 80px;
  height: 80px;
  margin-bottom: 10px;
}

.user-panel h3 {
  margin-bottom: 10px;
}

.user-panel textarea {
  width: 100%;
  height: 60px;
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  resize: none;
}

.user-panel button {
  width: 100%;
  padding: 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.user-panel button:hover {
  background-color: #0056b3;
}
</style>
