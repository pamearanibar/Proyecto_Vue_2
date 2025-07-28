<template>
  <div>
    <label>Buscar por nombre:</label>
    <input v-model="filtroNombre" placeholder="Buscar por nombre..." />

    <label>Filtrar por categoría:</label>
    <select v-model="filtroCategoria">
    <option value="">Todas</option>
    <option v-for="cat in categorias" :key="cat.id" :value="cat.id">{{ cat.nombre }}</option>
    </select>

    <EquipoForm 
      :modelValue="equipoActual"
      :categorias="categorias"
      @save="guardarEquipo"
    />
    <EquipoList 
       :equipos="equiposFiltrados"
       :categorias="categorias"
       @editar="editarEquipo"
       @eliminar="eliminarEquipo"
/>

  </div>
</template>

<script>
import axios from 'axios'
import EquipoForm from '../components/EquipoForm.vue'
import EquipoList from '../components/EquipoList.vue'

export default {
  components: { EquipoForm, EquipoList },
  data() {
     return {
        equipos: [],
        categorias: [],
        equipoActual: {
            nombre: '',
            marca: '',
            modelo: '',
            precio: 0,
            stock: 0,
            categoriaId: ''
        },
        filtroNombre: '',
        filtroCategoria: ''  
    }
  },

  computed: {
  equiposFiltrados() {
    return this.equipos.filter(e => {
      const coincideNombre = e.nombre.toLowerCase().includes(this.filtroNombre.toLowerCase());
      const coincideCategoria = !this.filtroCategoria || e.categoriaId === Number(this.filtroCategoria);
      return coincideNombre && coincideCategoria;
    });
    }
  },
  mounted() {
    this.obtenerEquipos()
    this.obtenerCategorias()
  },
  methods: {
    obtenerEquipos() {
      axios.get('http://localhost:3000/equipos').then(res => {
        this.equipos = res.data
      })
    },
    obtenerCategorias() {
      axios.get('http://localhost:3000/categorias').then(res => {
        this.categorias = res.data
      })
    },
    guardarEquipo(equipo) {
      if (equipo.id) {
        axios.put(`http://localhost:3000/equipos/${equipo.id}`, equipo).then(() => {
          this.obtenerEquipos()
        })
      } else {
        axios.post('http://localhost:3000/equipos', equipo).then(() => {
          this.obtenerEquipos()
        })
      }
      this.reiniciarFormulario()
    },
    editarEquipo(equipo) {
      this.equipoActual = { ...equipo }
    },
    eliminarEquipo(id) {
      axios.delete(`http://localhost:3000/equipos/${id}`).then(() => {
        this.obtenerEquipos()
      })
    },
    reiniciarFormulario() {
      this.equipoActual = {
        nombre: '',
        marca: '',
        modelo: '',
        precio: 0,
        stock: 0,
        categoriaId: ''
      }
    }
  }
}
</script>
