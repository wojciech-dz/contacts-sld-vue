<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
  <ContactsForm />
</template>

<script>
import ContactsForm from './ContactsForm.vue'


export default {
  name: 'ContactsData',
  components: {
    ContactsForm,
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
