<template>
  <form @submit.prevent="procesarFormulario">
    <Input :tarea="tarea" />
  </form>
  <hr>
 <ListaTareas/>
</template>

<script>

import Input from '../components/Input'
import {mapActions} from 'vuex'
import ListaTareas from '../components/ListaTareas';
const shortid = require('shortid');

export default {
  name: 'Home',
  components: {
    Input,
    ListaTareas
  },
  data() {
    return {
      tarea: {
        id:"",
        nombre:'',
        categorias: [],
        estado:'',
        numero:0,
      }
    }
  },
  methods: {
    ...mapActions(['setTareas']),

    procesarFormulario(){
      console.log(this.tarea);
      if(this.tarea.nombre.trim() === "") {
        console.log("El campo está vacío")
        return
      }
      console.log("No está vacio")

      // Generar id
          this.tarea.id = shortid.generate()
          console.log( this.tarea.id);
      // Envian los datos
          this.setTareas(this.tarea)

      // Limpiar datos
      this.tarea = {
        id:'',
        nombre:'',
        categorias: [],
        estado:'',
        numero:0,
      }
    }
  },
  
}
</script>
