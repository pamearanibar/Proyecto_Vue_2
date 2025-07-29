<template>
  <div >
    <h2 style="color: #ff880f;">{{ equipo.id ? 'Editar' : 'Nuevo' }} Equipo Médico</h2>
    <form @submit.prevent="guardar">
      <label> Nombre:
      <input v-model="equipo.nombre" placeholder="Nombre" required />
      </label>

      <label> Marca:
      <input v-model="equipo.marca" placeholder="Marca" />
      </label>

      <label> Modelo:
      <input v-model="equipo.modelo" placeholder="Modelo" />
      </label>

      <label> Precio:
      <input type="number" v-model="equipo.precio" placeholder="Precio" />
      </label>

      <label> Stock:
      <input type="number" v-model="equipo.stock" placeholder="Stock" />
      </label>

      <label> Categoría:
      <select v-model="equipo.categoriaId" required>
        <option disabled value="">Seleccione una categoría</option>
        <option v-for="cat in categorias" :key="cat.id" :value="cat.id">
          {{ cat.nombre }}
        </option>
      </select>
      </label>

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
