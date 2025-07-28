<template>
  <div>
    <h2>Listado de Equipos Médicos</h2>
    <table>
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Marca</th>
          <th>Modelo</th>
          <th>Precio</th>
          <th>Stock</th>
          <th>Categoría</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="equipo in equipos" :key="equipo.id">
          <td>{{ equipo.nombre }}</td>
          <td>{{ equipo.marca }}</td>
          <td>{{ equipo.modelo }}</td>
          <td>{{ equipo.precio }}</td>
          <td>{{ equipo.stock }}</td>
          <td>{{ obtenerNombreCategoria(equipo.categoriaId) }}</td>
          <td>
            <button @click="$emit('editar', equipo)">Editar</button>
            <button @click="$emit('eliminar', equipo.id)">Eliminar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: {
    equipos: Array,
    categorias: Array
  },
  methods: {
    obtenerNombreCategoria(id) {
      const cat = this.categorias.find(c => c.id === id);
      return cat ? cat.nombre : 'Sin categoría';
    }
  }
}
</script>
