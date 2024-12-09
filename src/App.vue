<template>
<div class="app">
  <div>
    <h1>Users</h1>
    <ul>
      <li v-for="user in users" :key="user.id">
        <p>User Name: {{ user.name }}</p>
        <p>User Age: {{ user.age }}</p>
        <p>Is Active: {{ user.isActive }}</p>
      </li>
    </ul>
  </div>
</div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
//
import db from '../firebase/config'
//
import { onSnapshot, collection, getDocs,   } from 'firebase/firestore'

const users = ref([])


onMounted(async () => {
  // Fetch data
  // const querySnapshot = await getDocs(collection(db, "users"))
  // users.value = querySnapshot.docs.map(doc => doc.data())
  // console.log("Users:", users.value)

  // Realtime data
  onSnapshot(collection(db, "users"), (querySnapshot) => {
    users.value = querySnapshot.docs.map(doc => doc.data())
    console.log("Users:", users.value)
  })
})

</script>

<style scoped>
.app{
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>