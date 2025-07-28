<template>
  <div>
    <h1>Importadora de Equipos Médicos</h1>
    <EquiposView />
    <CategoriasView />
  </div>
</template>

<script>
import EquiposView from './views/EquiposView.vue'
import CategoriasView from './views/CategoriasView.vue'

export default {
  components: {
    EquiposView,
    CategoriasView
  }
}
</script>
