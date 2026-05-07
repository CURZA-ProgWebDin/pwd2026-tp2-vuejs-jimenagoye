<script setup>
import { ref, computed } from 'vue';
import ProductForm from './components/ProductForm.vue';
import ProductList from './components/ProductList.vue';

const productos = ref([]);
const proximoId = ref(1);

const crearProducto = (nuevoProducto) => {
  const productoConId = { ...nuevoProducto, id: proximoId.value };
  productos.value.push(productoConId);
  proximoId.value++; 
};

const eliminarProducto = (id) => {
  productos.value = productos.value.filter(p => p.id !== id);
};
const cantidadTotal = computed(() => {
  return productos.value.reduce((total, p) => total + Number(p.stock), 0);
});

const valorTotalInventario = computed(() => {
  return productos.value.reduce((total, p) => total + (Number(p.precio) * Number(p.stock)), 0);
});
</script>
<template>
  <main class="contenedor-tp">
    <header>
      <h1>Gestión de Productos</h1>
    </header>

    <div class="seccion-superior">
      <div class="caja-blanca">
        <ProductForm @add-product="crearProducto" />
      </div>

      <div v-if="productos.length > 0" class="resumen-container">
        <h3>Resumen del Inventario</h3>
        <div class="resumen-item">
          <span>Cantidad total:</span>
          <strong>{{ cantidadTotal }}</strong>
        </div>
        <div class="resumen-item">
          <span>Valor total:</span>
          <strong>${{ valorTotalInventario }}</strong>
        </div>
      </div>
    </div>
    <div class="caja-blanca">
      <div class="scroll-interno">
        <ProductList :productos="productos" @delete-product="eliminarProducto" />
      </div> <!-- 2. Cerramos el div -->
    </div>
  </main>
</template>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: #DBA9AB;
  min-height: 100vh;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #4a3435;
}

.contenedor-tp {
  max-width: 1100px;
  margin: 0 auto;
  padding: 40px 20px;
  display: flex;
  flex-direction: column;
  gap: 30px;
}
header {
  display: flex;
  justify-content: center;
  margin-bottom: 10px;
}

h1 {
  background-color: (#a42195);
  padding: 15px 40px;
  border-radius: 60px;
  font-size: 2.8rem;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
  margin: 0;
  display: inline-block;
  border: 1px solid rgba(216, 17, 166, 0.2);
  background-color: white;
  color: #3e2723;
  border: 2px solid #5b3655;
  padding: 15px 40px;
  border-radius: 60px;
  h1 {
  background-color: white;
  color: #4a3435;
  border: 2px solid #8b5a5c;
  padding: 15px 40px;
  border-radius: 60px;
}
}
.seccion-superior {
  display: flex;
  flex-direction: row;
  align-items: stretch;
  gap: 30px;
  width: 100%;
}

.caja-blanca {
  flex: 1.5;
  background: white;
  padding: 30px;
  border-radius: 20px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.08);
}
.resumen-container {
  flex: 1;
  background-color: #f9ecee;
  padding: 30px;
  border-radius: 20px;
  border: 1px solid #8b5a5c;
  text-align: center;
  box-shadow: 0 4px 20px rgba(0,0,0,0.08);
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.resumen-container h3 {
  margin-top: 0;
  font-size: 1.5rem;
  border-bottom: 1px solid rgba(139, 90, 92, 0.3);
  padding-bottom: 10px;
}

.resumen-item {
  margin: 20px 0;
  font-size: 1.2rem;
}

.resumen-item strong {
  color: #8b5a5c;
  font-size: 2rem;
  display: block;
  margin-top: 5px;
}
@media (max-width: 850px) {
  .seccion-superior {
    flex-direction: column;
  }
  h1 {
    font-size: 2rem;
    padding: 10px 25px;
  }
}
table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 10px;
}

table th, table td {
  padding: 15px;
  text-align: center;
  vertical-align: middle;
  color: #4a3435;
}
table td:nth-child(2) {
  padding-left: 30px; 
}
table thead tr {
  border-bottom: 2px solid #DBA9AB;
}
.caja-blanca:hover, .resumen-container:hover {
  transform: translateY(-5px);
  transition: all 0.3s ease;
  box-shadow: 0 8px 25px rgba(0,0,0,0.15);
}
input:focus, select:focus {
  outline: none;
  border-color: #8b5a5c !important;
  box-shadow: 0 0 5px rgba(139, 90, 92, 0.4);
  transition: all 0.3s ease;
}
.caja-blanca:hover, .resumen-container:hover {
  transform: translateY(-5px);
  transition: all 0.3s ease;
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}
.scroll-interno {
  max-height: 450px;
  overflow-y: auto;
  overflow-x: hidden;
  padding-right: 10px;
}
table thead {
  position: sticky;
  top: 0;
  background-color: white;
  z-index: 10;
}

/* Diseño de la barrita de scroll para que no quede la gris fea */
.scroll-interno::-webkit-scrollbar {
  width: 8px;
}
.scroll-interno::-webkit-scrollbar-thumb {
  background: #DBA9AB; /* Tu color rosa viejo */
  border-radius: 10px;
}
.scroll-interno::-webkit-scrollbar-track {
  background: #f9ecee;
}
</style>