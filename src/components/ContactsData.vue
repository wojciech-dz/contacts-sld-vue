<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
  <ContactsForm />
  <ContactsList />
</template>

<script>
import ContactsForm from './ContactsForm.vue'
// import ContactsList from './ContactsList.vue'

export default {
  name: 'ContactsData',
  components: {
    ContactsForm,
    // ContactsList
  },
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
