<template>
    <div class="obtener-usuario">
      <button @click="obtenerUsuario">Obtener Usuarios</button>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  
  export default {
    methods: {
      async obtenerUsuario() {
        try {
          const response = await axios.get("https://randomuser.me/api/?results=2");
          const users = response.data.results.map((user) => ({
            name: `${user.name.first} ${user.name.last}`,
            picture: user.picture.thumbnail,
            color: this.colorAleatorio(),
          }));
          this.$emit("users-fetched", users); // Emitir los usuarios obtenidos
        } catch (error) {
          console.error("Error al obtener usuarios:", error);
          
        }
      },
      colorAleatorio() {
        const colors = ["#FF5733", "#33FF57", "#3357FF", "#C7C223", "#FF33A1"];
        return colors[Math.floor(Math.random() * colors.length)];
      },
    },
  };
  </script>
  
  <style scoped>
  .obtener-usuario {
    margin: 20px 0;
  }
  button {
    padding: 10px 20px;
    cursor: pointer;
    background-color: #007bff;
    color: #fff;
    border: none;
    border-radius: 5px;
  }
  button:hover {
    background-color: #0056b3;
  }
  </style>
  