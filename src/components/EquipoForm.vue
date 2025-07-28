<template>
  <div>
    <h2>{{ equipo.id ? 'Editar' : 'Nuevo' }} Equipo Médico</h2>
    <form @submit.prevent="guardar">
      <label>Nombre:</label>
      <input v-model="equipo.nombre" placeholder="Nombre" required />

      <label>Marca:</label>
      <input v-model="equipo.marca" placeholder="Marca" />

      <label>Modelo:</label>
      <input v-model="equipo.modelo" placeholder="Modelo" />

      <label>Precio:</label>
      <input type="number" v-model="equipo.precio" placeholder="Precio" />

      <label>Stock:</label>
      <input type="number" v-model="equipo.stock" placeholder="Stock" />

      <label>Categoría:</label>
      <select v-model="equipo.categoriaId" required>
        <option disabled value="">Seleccione una categoría</option>
        <option v-for="cat in categorias" :key="cat.id" :value="cat.id">
          {{ cat.nombre }}
        </option>
      </select>

      <br><br>
      <button type="submit">Guardar</button>
    </form>
  </div>
</template>


<script>
export default {
  props: {
    modelValue: Object,
    categorias: Array
  },
  emits: ['save'],
  data() {
    return {
      equipo: { ...this.modelValue }
    };
  },
  watch: {
    modelValue(newVal) {
      this.equipo = { ...newVal };
    }
  },
  methods: {
    guardar() {
      this.$emit('save', this.equipo);
    }
  }
}
</script>
