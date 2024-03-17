<script setup>
  import { ref, computed } from 'vue'
  import axios from 'axios'

  const name = ref('')
  const surname = ref('')
  const email = ref('')
  const contents = ref('')
  const contactData = ref(null)

  const cantSave = computed(
    () => !name.value || !surname.value || !email.value || !contents.value || !validEmail(email.value)
  )

  async function saveForm() {
    alert(`Zapisujesz ${name.value}`)
    // contactData.value = await response.json()
    try {
      const response = await axios.post('https://localhost:8001/contactform', {
            message: name.value
          });
      console.log(response.data)
      contactData.value = response.data
    } catch (error){
      console.log(error)
    }
    // console.log(response.error)
    // contactData.value = response.data
  }

  // async sendData() {
  //   try {
  //     const response = await axios.post('http://localhost:8000/contact', {
  //       data: name
  //     });

  //     console.log(response.data);
  //   } catch (error) {
  //     console.error(error);
  //   }
  // }

  function validEmail(email) {
    var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test(email);
  }

  // const requestOptions = {
  //     method: "POST",
  //     headers: { "Content-Type": "application/json" },
  //     body: JSON.stringify({ name: "Vue 3 POST Request Example" })
  //     // body: JSON.stringify(
  //     //   { name: name.value }
  //     //   { surname: surname.value }
  //     //   { email: email.value }
  //     //   { contents: contents.value }
  //     //   )
  //   }

  // const response = await fetch('http://localhost:8000/contact', requestOptions)
  // const data = await response.json()
  // contactData.value = data
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
  <div class="savedContact">
      <div class="savedContact email">New product email: {{contact?.email}}</div>
  </div>
</template>

<script>
export default {
  name: 'ContactsForm',
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h4 {
  margin: 10 0 0 0;
}
</style>
