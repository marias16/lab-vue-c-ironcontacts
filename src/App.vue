<template>
  <table>
    <tr>
      <th>Picture</th>
      <th>Name</th>
      <th>Popularity</th>
    </tr>
    <tr v-for="contact in contacts" :key="contact.id">
      <td><img :src="contact.pictureUrl"></td>
      <td>{{ contact.name }}</td>
      <td>{{ contact.popularity }}</td>
    </tr>
  </table>
</template>

<script setup>
import ContactList from './contacts.json'
import { ref } from 'vue'
const contacts = ref(ContactList.slice(0, 5))
</script>

<style scoped>
table {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

img {
  width: 100px;
}
</style>
