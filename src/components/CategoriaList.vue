<template>
  <div>
    <h2>Lista de Categorías</h2>
    <table border="1">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="categoria in categorias" :key="categoria.id">
          <td>{{ categoria.nombre }}</td>
          <td>
            <button @click="$emit('editar', categoria)">Editar</button>
            <button @click="$emit('eliminar', categoria.id)">Eliminar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    categorias: Array
  },
  emits: ['editar', 'eliminar']
}
</script>
