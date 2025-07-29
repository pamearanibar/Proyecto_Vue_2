<template>
  <div>
    <h2 style="color: #ff880f;">Nueva Categoría</h2>
    <input v-model="localCategoria.nombre" placeholder="Nombre de la categoría" />
    <button @click="guardar">Guardar</button>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: Object
  },
  emits: ['save'],
  data() {
    return {
      localCategoria: {
        nombre: ''
      }
    }
  },
  watch: {
    modelValue: {
      immediate: true,
      handler(val) {
        this.localCategoria = val ? { ...val } : { nombre: '' };
      }
    }
  },
  methods: {
    guardar() {
      this.$emit('save', { ...this.localCategoria });
      this.localCategoria = { nombre: '' };
    }
  }
}
</script>
