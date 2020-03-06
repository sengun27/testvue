<template>
  <div id="app" class="small-container">
    <h1>Table</h1>
    <StudentForm @add="addElement"/>
    <StudentTable 
      v-bind:elements="elements" 
      @delete="deleteElement"
      @edit="editElement"
    />
  </div>
</template>

<script>
import StudentTable from './components/Table.vue'
import StudentForm from './components/Form.vue'

export default {
  name: 'App',
  components: {
    StudentTable,
    StudentForm,
  },
  data() {
    return {
      elements: [
        {
          id: 1,
          name: 'Yamamoto Taro',
          email: 'taro@sample.co.jp',
        },
      ],
    }
  },
  methods :{
    addElement(e){
      const id = this.elements.length + 1
      const newElement = {...e, id}
      this.elements = [...this.elements, newElement]
    },
    deleteElement(id) {
      this.elements = this.elements.filter(
        e => e.id !== id
      )
    },
    editElement(id, element){
      this.elements == this.elements.map(e =>
        e.id === id ? element : e
      )
    },
  }
}
</script>

<style>
button {
    background: #009435;
    border: 1px solid #009435;
}

.small-container {
    max-width: 680px;
}
</style>
