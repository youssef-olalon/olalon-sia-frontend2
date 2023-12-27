<script>

export default {
  data() {
  return {
    users: [
      { id: 1, name: 'cliente 1', email: 'usuario1@example.com' },
      { id: 2, name: 'cliente 2', email: 'usuario2@example.com' },
      // ++
    ],
    search: "",
    messageDialog: false,
    editDialog: false,
    message: '', // Mensaje a enviar
  };
},

  computed: {
    // Filtra los clientes basados en la búsqueda
    filteredUsers() {
      return this.users.filter(obj =>
        Object.values(obj).some(val =>
          String(val).toLowerCase().includes(this.search.toLowerCase())
        )
      );
    },
  },
  methods: {
    // Lógica para enviar mensaje al cliente
    sendMessage(userId) {
      // Imprime el mensaje en la consola por ahora
      console.log('Mensaje enviado:', this.message);
      this.messageDialog = false; // Cierra el modal después de enviar el mensaje
    },
    // Lógica para editar compras del cliente
    editPurchases(userId) {
      this.editDialog = false; 
    },
  },
};
</script>

<template>
  <v-container class="" style="background-color: white;">
    <!-- Encabezado con el logo -->
    <v-row>
      <v-col cols="22" class="header" style="background-color: white;">
        <v-img src="olalon-logo.webp" alt="Logo" class="logo"></v-img>
        <v-btn> Cerrar sesíon</v-btn>
      </v-col>
    </v-row>

    <!-- Lista de clientes -->
    <v-row>
      <v-col cols="12" class="cliente-card" v-for="(user, index) in filteredUsers" :key="index">
        <v-card class="container__clients">
          <!-- Detalles del cliente -->
          <v-card-title>{{ user.name }}</v-card-title>
          <v-card-text>
            <p>Correo electrónico: {{ user.email }}</p>
            <!-- Otros detalles del cliente: dirección- compras- etc -->
          </v-card-text>
          <v-card-actions>
            <v-btn @click="sendMessage(user.id)">Enviar Mensaje</v-btn>
            <v-btn @click="editPurchases(user.id)">Editar Compras</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>


<style scoped>
.header {
  text-align: center;
  padding: 20px 0;
  display: flex;
  flex-direction: row;
  gap: 900px;
}
.logo {
  width: 200px;
  height: 100px;
  border-radius: 30px;
}
.container__clients {
  display: flex;
  width: min-content;
  flex-direction: column;
  gap: 50px;
}
</style>
