<template>
<div id="studnet-table">
    <table>
      <thead>
        <th>Student Name</th>
        <th>Student Email</th>
        <th></th>
      </thead>
      <tbody>
        <tr v-for="element in elements" :key="element.id">
          <td v-if="editing === element.id">
            <input type="text" v-model="element.name" />
          </td>
          <td v-else>{{ element.name }}</td>
          <td v-if="editing === element.id">
            <input type="text" v-model="element.email" />
          </td>
          <td v-else>{{ element.email }}</td>
          <td v-if="editing === element.id">
            <button @click="editElement(element)">Save</button>
            <button class="muted-button" @click="cancel(element)">Cancel</button>
          </td>
          <td v-else>
            <button @click="edit(element)">Edit</button>
            <button @click="$emit('delete',element.id)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
</div>
</template>

<script>
  export default {
    name: 'student-table',
    props: {
      elements : Array,
    }, 
    data(){
      return {
        editing: null
      }
    },
    methods: {
      edit(element){
        this.cachedElement = Object.assign({}, element)
        this.editing = element.id
      },
      editElement(element){
        this.$emit('edit:', element.id, element)
        this.editing = null
      },
      cancel(element){
        Object.assign(element, this.cachedElement)
        this.editing = null
      }
      
    }
  }
</script>

<style scoped>
  button {
    margin: 0 0.5rem 0 0;
  }
</style>
