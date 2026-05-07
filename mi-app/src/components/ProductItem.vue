<script setup>
defineProps(['producto']);
const emit = defineEmits(['delete-product']);
</script>

<template>
  <tr class="itemProducto">
    <td>{{ producto.id }}</td> 
    <td>{{ producto.nombre }}</td>
    <td>{{ producto.precio }}</td>
    <td>{{ producto.stock }}</td>
    <td>{{ producto.categoria }}</td>
    <td>
      <button @click="emit('delete-product', producto.id)" class="btn-borrar">
        🗑️
      </button>
    </td>
  </tr>
</template>

<style scoped>
.btn-borrar {
  background-color: #ff4d4d;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 4px;
  cursor: pointer;
  transition: background 0.3s;
}

.btn-borrar:hover {
  background-color: #cc0000;
}

.itemProducto td {
  padding: 10px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  color: #4a3435;
}
</style>