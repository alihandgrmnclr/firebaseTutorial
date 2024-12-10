<template>
<div class="app">
  <h1>Users</h1>
  <!-- User List -->
  <div class="list">
    <UserList
      :users="users"
      @updateUser="updateUser"
      @deleteUser="deleteUser"
    />
  </div>
  
  <!-- Add New User -->
  <CreateForm @addUser="createUser" />
</div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
//
import db from '../firebase/config'
//
import { doc, onSnapshot, collection, addDoc, deleteDoc, updateDoc } from 'firebase/firestore'
//
import CreateForm from './components/CreateForm.vue'
import UserList from './components/UserList.vue'

const users = ref([])

function createUser(user) {
  addDoc(collection(db, "users"), {
    name: user.name,
    age: user.age,
    isActive: user.isActive,
    id: user.id
  })
}
function updateUser(user) {
  updateDoc(doc(db, "users", user.docId), {
    name: user.name,
    age: user.age,
    isActive: user.isActive
  })
}
async function deleteUser(id) {
  await deleteDoc(doc(db, "users", id))
  alert('User deleted successfully')
}

onMounted(async () => {
  // Realtime data
  onSnapshot(collection(db, "users"), (querySnapshot) => {
    users.value = []
    querySnapshot.forEach((doc) => {
      users.value.push({
        docId: doc.id,
        ...doc.data()
      })
    })
  })
})

</script>

<style scoped>
.app{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.list {
  max-height: 700px;
  overflow: auto;
}
</style>