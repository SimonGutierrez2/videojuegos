<script setup>
import { ref, computed } from 'vue';

let juego = ref({
  nombre: "",
  plataforma: "",
  estado: "",
  puntaje: "",
});

let nombrefiltrado = ref("");
let plataformafiltrado = ref("");
let estadofiltrado = ref("");
let juegos = ref([]);
let juegoSeleccionado = ref(null);

function agregarjueguito() {
  juegos.value.push({
    nombre: juego.value.nombre,
    plataforma: juego.value.plataforma,
    estado: juego.value.estado,
    puntaje: juego.value.puntaje,
  });

  juego.value.nombre = "";
  juego.value.plataforma = "";
  juego.value.estado = "";
  juego.value.puntaje = "";
}

function mostrarFila(juegoSeleccionadoParam) {
  juegoSeleccionado.value = { ...juegoSeleccionadoParam };
}

const juegosFiltrados = computed(() => {
  return juegos.value.filter(juego => {
    return (
      (!nombrefiltrado.value || juego.nombre.toLowerCase().includes(nombrefiltrado.value.toLowerCase())) &&
      (!plataformafiltrado.value || juego.plataforma === plataformafiltrado.value) &&
      (!estadofiltrado.value || juego.estado === estadofiltrado.value)
    );
  });
});
</script>

<template>
  <div class="container">
    <h1 class="title">🎄 Nuevo Videojuego 🎄</h1>
    <form @submit.prevent class="form">
      <label for="">Nombre</label>
      <input type="text" v-model="juego.nombre" class="input"><br>
      
      <label for="">Plataforma</label>
      <select v-model="juego.plataforma" class="select">
        <option value="">Elegir</option>
        <option value="PC">PC</option>
        <option value="Play">Play</option>
        <option value="Xbox">Xbox</option>
      </select><br>
      
      <label for="">Estado</label>
      <input type="text" v-model="juego.estado" class="input"><br>
      
      <label for="">Puntaje</label>
      <input type="text" v-model="juego.puntaje" class="input"><br>
      
      <input type="button" @click="agregarjueguito" value="Registrar videojuego" class="button"><br><br>
    </form>

    <h1 class="title">🎮 Videojuegos 🎮</h1>

    <label for="">Nombre</label>
    <input type="text" v-model="nombrefiltrado" class="input">
    
    <label for="">Plataforma</label>
    <select v-model="plataformafiltrado" class="select">
      <option value="">Todos</option>
      <option value="PC">PC</option>
      <option value="Play">Play</option>
      <option value="Xbox">Xbox</option>
    </select>
    
    <label for="">Estado</label>
    <select v-model="estadofiltrado" class="select">
      <option value="">Todos</option>
      <option value="Jugando">Jugando</option>
      <option value="Completado">Completado</option>
      <option value="Pendiente">Pendiente</option>
    </select>

    <table class="table">
      <tr>
        <th>Nombre</th>
        <th>Plataforma</th>
        <th>Estado</th>
        <th>Puntaje</th>
        <th>+info</th>
      </tr>
      <tr v-for="sorete in juegosFiltrados" :key="sorete.nombre">
        <td>{{ sorete.nombre }}</td>
        <td>{{ sorete.plataforma }}</td>
        <td>{{ sorete.estado }}</td>
        <td>{{ sorete.puntaje }}</td>
        <td><button @click="mostrarFila(sorete)" class="info-button">+info</button></td>
      </tr>
    </table>

    <h1 class="title">🎁 FILTRO 🎁</h1>
    <div v-if="juegoSeleccionado">
      <table class="info-table">
        <tr>
          <th>Nombre</th>
          <th>Plataforma</th>
          <th>Estado</th>
          <th>Puntaje</th>
        </tr>
        <tr>
          <td>{{ juegoSeleccionado.nombre }}</td>
          <td>{{ juegoSeleccionado.plataforma }}</td>
          <td>{{ juegoSeleccionado.estado }}</td>
          <td>{{ juegoSeleccionado.puntaje }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<style scoped>
.container {
  background-color: #f9f9f9;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.title {
  text-align: center;
  color: #ff4d4d;
  font-family: 'Cursive', sans-serif;
  margin-bottom: 20px;
}

.form, .input, .select, .button {
  margin: 10px;
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ddd;
}

.input, .select {
  width: calc(100% - 24px);
}

.button {
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}

.button:hover {
  background-color: #45a049;
}

.table, .info-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

.table th, .table td, .info-table th, .info-table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

.info-button {
  background-color: #ffcc00;
  border: none;
  cursor: pointer;
  padding: 5px 10px;
  border-radius: 5px;
}

.info-button:hover {
  background-color: #ffbb00;
}
</style>
