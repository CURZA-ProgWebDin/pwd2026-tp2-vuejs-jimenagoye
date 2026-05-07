<script setup>
import { ref } from 'vue';
const emit = defineEmits(['add-product']);
const nombre = ref('');
const precio = ref(0);
const stock = ref(0);
const categoria = ref('');
const handleSubmit = () => {
  if (nombre.value.trim() === '' || precio.value <= 0 || stock.value <= 0 || categoria.value === '') {
    alert('Por favor, completa todos los campos con valores válidos.');
    return;
  }

  const nuevoProducto = {
    nombre: nombre.value,
    precio: precio.value,
    stock: stock.value,
    categoria: categoria.value
  };

  emit('add-product', nuevoProducto);

  nombre.value = '';
  precio.value = 0;
  stock.value = 0;
  categoria.value = '';
};
</script>

<template>
  <div class="formulario">
    <h3>Cargar Nuevo Producto</h3>
    <form @submit.prevent="handleSubmit">
      <div class="campo">
        <label>Nombre del producto:</label>
        <input v-model="nombre" type="text" placeholder="Ej: Perfume Amour" />
      </div>

      <div class="campo">
        <label>Precio:</label>
        <input v-model.number="precio" type="number" step="0.01" />
      </div>

      <div class="campo">
        <label>Stock:</label>
        <input v-model.number="stock" type="number" />
      </div>

      <div class="campo">
        <label>Categoría:</label>
        <select v-model="categoria">
          <option disabled value="">Seleccione una categoría</option>
          <option value="Fragancias">Fragancias</option>
          <option value="Hogar">Hogar</option>
          <option value="Limpieza">Limpieza</option>
        </select>
      </div>

      <button type="submit">Guardar Producto</button>
    </form>
  </div>
</template>

<style scoped>
.formulario {
  background: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
  border: 1px solid #ddd;
  margin-bottom: 20px;
}
.campo {
  margin-bottom: 15px;
  display: flex;
  flex-direction: column;
}
label {
  font-weight: bold;
  margin-bottom: 5px;
}
input, select {
  padding: 8px;
  border: 1px solid #4b2a42;
  border-radius: 4px;
}
button {
  background-color: #a0467f;
  color: white;
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  width: 100%;
}
button:hover {
  background-color: #7b326c;
}
</style>