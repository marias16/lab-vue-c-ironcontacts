<template>
  <button @click="addRandom">Add new random contact</button>
  <button @click="sortPopularity">Sort by popularity</button>
  <button @click="sortName">Sort by name</button>
  <table>
    <tr>
      <th>Picture</th>
      <th>Name</th>
      <th>Popularity</th>
      <th>Won an Oscar</th>
      <th>Won an Emmy</th>
    </tr>
    <tr v-for="contact in contacts" :key="contact.id">
      <td><img :src="contact.pictureUrl"></td>
      <td>{{ contact.name }}</td>
      <td>{{ contact.popularity }}</td>
      <td><p v-if="contact.wonOscar">🏆</p></td>
      <td><p v-if="contact.wonEmmy">🏆</p></td>
      <td><button @click="deleteRow(contact.id)">Delete contact</button></td>
    </tr>
  </table>
  <button @click="addRandom">Add new random contact</button>
  <button @click="sortPopularity">Sort by popularity</button>
  <button @click="sortName">Sort by name</button>
</template>

<script setup>
import ContactList from './contacts.json'
import { ref } from 'vue'

//iteration 1
const contacts = ref(ContactList.slice(0, 5))

//iteration 3
let newContactList = ContactList.slice(5, ContactList.length)
function addRandom () {
  if(!newContactList.length) {
    return null
  }
  const randomNumber = Math.floor(Math.random() * (newContactList.length - 1))
  const randomContact = newContactList[randomNumber]
  contacts.value.push(randomContact)
  newContactList = newContactList.filter(contact => contact !== randomContact)
}

//iteration 4
function sortPopularity() {
  contacts.value.sort((a, b) => b.popularity -a.popularity)
}

function sortName() {
  contacts.value.sort((a, b) => a.name.localeCompare(b.name))
}

//iteration 5 
function deleteRow(contactId) {
  if(contacts.value.length === 1) {
    newContactList = ContactList;
  }
  contacts.value = contacts.value.filter(contact => contact.id !== contactId)
}
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
