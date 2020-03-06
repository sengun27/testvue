<template>
  <div id="element-form">
    <form @submit.prevent="handleSubmit">
      <label>Student Name</label>
      <input v-model="element.name"
             type="text" 
             :class="{ 'has-error': submitting && invalidName}"
             @focus="clearStatus"
             @keypress="clearStatus"
      />
      <label>Studnet Email</label>
      <input v-model="element.email"
             type="text" 
             :class="{ 'has-error': submitting && invalidEmail}"
             @focus="clearStatus"
      />
      <p v-if="error && submitting" class="error-message">
        please fill out all required fields correctly
      </p>
      <p v-if="success" class="success-message">
        successfully added
      </p>
      <button>Add Studnet</button>
    </form>
  </div>
</template>

<script>
  export default {
    name: 'element-form',
    data() {
      return {
        submitting: false,
        error: false,
        success: false,
        element: {
          name: '',
          email: '',
        },
        reg: /^([A-Za-z0-9_\-.])+@([A-Za-z0-9_\-.])+\.([A-Za-z]{2,4})$/
      }
    },
    computed: {
      invalidName(){
        console.log(this.element.name === '')
        return this.element.name === ''
      },
      invalidEmail(){
        if(!this.reg.test(this.element.email)){
          console.log("ok")
          return true
        }
        return false
      },
    },
    methods: {
      handleSubmit(){
        this.submitting = true
        this.clearStatus()

        if(this.invalidName || this.invalidEmail){
          this.error = true
          return
        }
        this.$emit('add',this.element)
        this.clearElement()
        this.error = false
        this.success = true
        this.submitting = false

      },
      clearStatus(){
        this.success = false
        this.error = false
      },
      clearElement(){
        this.element = {
          name: '',
          email: '',
        }
      }
    },
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>
