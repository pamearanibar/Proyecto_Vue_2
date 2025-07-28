<template>
  <div>
    <CategoriaForm 
      :modelValue="categoriaActual"
      @save="guardarCategoria"
    />
    <CategoriaList 
      :categorias="categorias"
      @editar="editarCategoria"
      @eliminar="eliminarCategoria"
    />
  </div>
</template>

<script>
import axios from 'axios'
import CategoriaForm from '../components/CategoriaForm.vue'
import CategoriaList from '../components/CategoriaList.vue'

export default {
  components: { CategoriaForm, CategoriaList },
  data() {
    return {
      categorias: [],
      categoriaActual: { nombre: '' }
    }
  },
  mounted() {
    this.obtenerCategorias()
  },
  methods: {
    obtenerCategorias() {
      axios.get('http://localhost:3000/categorias').then(res => {
        this.categorias = res.data
      })
    },
    guardarCategoria(categoria) {
       if (categoria.id) {
    axios.put(`http://localhost:3000/categorias/${categoria.id}`, categoria).then(() => {
      this.obtenerCategorias()
    })
  } else {
    axios.post('http://localhost:3000/categorias', categoria).then(() => {
      this.obtenerCategorias()
    })
  }
  this.categoriaActual = { nombre: '' }
    },
    editarCategoria(categoria) {
      this.categoriaActual = { ...categoria }
    },
    eliminarCategoria(id) {
      axios.delete(`http://localhost:3000/categorias/${id}`).then(() => {
        this.obtenerCategorias()
      })
    }
  }
}
</script>
