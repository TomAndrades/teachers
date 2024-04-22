<template>
  <section>
    <h3>Añadir profesor</h3>
    <div><label>Nombre: </label> <input type="text" v-model="teacher.firstName" /></div>
    <div><label>Apellido: </label> <input type="text" v-model="teacher.lastName" /></div>
    <div><label>Dni: </label> <input type="text" v-model="teacher.dni" /></div>
    <div>
      <label>Materias: </label> 
      <input type="text" v-model="materia" /><button
        @click="agregarMateria">
        Agregar
      </button>
      <ul>
        <li v-for="(elm, i) in teacher.materias" :key="i">{{ elm }}</li>
      </ul>
    </div>
    <input type="checkbox" v-model="teacher.documentacion" /> Presenta toda la documentación?
    <button @click="agregarTeacher">Enviar</button>
  </section>
  <section>
    <h3>Lista de profesores</h3>
    <ul>
      <li v-for="teacher in teachers" :key="teacher.dni">{{ teacher }}</li>
    </ul>
  </section>
</template>

<script lang="ts" setup>
import { ref, type Ref } from 'vue'
interface ITeacher {
  firstName: string
  lastName: string
  dni: string
  materias: Array<string>
  documentacion: boolean
}
let teacher: Ref<ITeacher> = ref({
  firstName: '',
  lastName: '',
  dni: '',
  materias: [],
  documentacion: false
})
let teachers: Ref<Array<ITeacher>> = ref([])
let materia: Ref<string> = ref('')

const agregarMateria = () => {
  teacher.value.materias.push(materia.value)
  materia.value = ''
}

const agregarTeacher = () => {
  teachers.value.push(teacher.value)
  teacher.value = {
    firstName: '',
    lastName: '',
    dni: '',
    materias: [],
    documentacion: false
  }
}
</script>

<style scoped></style>
