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
      // Implementa la lógica para enviar mensaje al cliente con ID 'userId'
    },
    // Lógica para editar compras del cliente
    editPurchases(userId) {
      // Implementa la lógica para editar las compras del cliente con ID 'userId'
    },
  },
};
</script>

<template>
  <v-container class="v-container">
    <!-- Encabezado con el logo -->
    <v-row>
      <v-col cols="12" class="header">
        <v-img src="olalon-logo.webp" alt="Logo" class="logo"></v-img>
        <v-btn> Cerrar sesíon</v-btn>
      </v-col>
    </v-row>

    <!-- Lista de clientes -->
    <v-row>
      <v-col cols="12" class="cliente-card" v-for="(user, index) in filteredUsers" :key="index">
        <v-card>
          <!-- Detalles del cliente -->
          <v-card-title>{{ user.name }}</v-card-title>
          <v-card-text>
            <p>Correo electrónico: {{ user.email }}</p>
            <!-- Otros detalles del cliente: dirección- compras- etc -->
          </v-card-text>
          <!-- Botones de acción para el cliente -->
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
}

</style>

