<script setup>
import { ref, computed } from 'vue';
import ProductItem from './ProductItem.vue';
const props = defineProps(['productos']);
const emit = defineEmits(['delete-product']);
const filtro = ref('Todos');

const productos = computed(() => {
    if (filtro.value === 'Todos')
        return props.productos;
    return props.productos.filter(p => p.categoria === filtro.value);
});
</script>

<template>
  <div class="list-container">
    <label>Filtrar por: </label>
    <select v-model="filtro">
      <option value="Todos">Todos</option>
      <option value="Fragancias">Fragancias</option>
      <option value="Hogar">Hogar</option>
      <option value="Limpieza">Limpieza</option>
    </select>
  </div>

  <div v-if="productos.length > 0" class="lista">
    <table class="tablaProductos">
      <thead>
        <tr>
          <th>ID</th>
          <th>NOMBRE</th>
          <th>PRECIO</th>
          <th>STOCK</th>
          <th>CATEGORIA</th>
          <th>ELIMINAR</th>
        </tr>
      </thead>
      <tbody>
        <ProductItem 
            v-for="prod in productos" 
            :key="prod.id" 
            :producto="prod"
            @delete-product="(id) => $emit('delete-product', id)"                
        />
      </tbody>
    </table>
  </div>
  <p v-else class="mensajeVacio">No hay productos cargados</p>
</template>

<style scoped>
.lista {
  margin-top: 20px;
  background-color: white;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.tablaProductos {
  width: 100%;
  border-collapse: collapse;
}

.tablaProductos th {
  border-bottom: 2px solid #DBA9AB;
  padding: 10px;
  color: #4a3435;
}
</style>