<script setup>
  import { ref, computed } from 'vue'
  import axios from 'axios'

  const name = ref('')
  const surname = ref('')
  const email = ref('')
  const contents = ref('')
  const _name = ref('')
  const _surname = ref('')
  const _email = ref('')
  const _contents = ref('')

  const cantSave = computed(
    () => !name.value || !surname.value || !email.value || !contents.value || !validEmail(email.value)
  )

  async function saveForm() {
    try {
      const response = await axios.post('http://localhost:8001/contactform', {
            name: name.value,
            surname: surname.value,
            email: email.value,
            contents: contents.value,
          });
      _name.value = response.data.name
      _surname.value = response.data.surname
      _email.value = response.data.email
      _contents.value = response.data.contents
    } catch (error){
      console.log(error)
    }
  }

  function validEmail(email) {
    var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test(email);
  }
</script>

<template>
  <div class="form">
    <p>Imię: {{ name }}</p>
    Imię: <input v-model="name" placeholder="Imię" />
    <p>Nazwisko: {{ surname }}</p>
    Nazwisko: <input v-model="surname" placeholder="Nazwisko" />
    <p>Adres email: {{ email }}</p>
    Adres email: <input v-model="email" type="email" placeholder="Adres email" />
    <p>Treść: {{ contents }}</p>
    Treść: <input v-model="contents" placeholder="Wiadomość" />
  </div>
  
  <button :disabled="cantSave" @click="saveForm">Zapisz</button>
  
  <div v-show="_email && _email">
    <table>
        <tr><td>Imię</td><td>{{_name && _name}}</td></tr>
        <tr><td>Nazwisko</td><td>{{_surname && _surname}}</td></tr>
        <tr><td>Adres email</td><td>{{_email && _email}}</td></tr>
        <tr><td>Wiadomość</td><td>{{_contents && _contents}}</td></tr>
    </table>
  </div>

</template>

<script>
export default {
  name: 'ContactsForm',
}
</script>

<style scoped>
h4 {
  margin: 10 0 0 0;
}
</style>
