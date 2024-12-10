<template>
<div>
  <ul class="users-list">
    <li class="users" v-for="user in users" :key="user.id">
      <div class="users_info">
        <span>User Name:</span>
        <input
          class="user_name"
          type="text"
          v-model="user.name"
          />
      </div>
      <div class="users_info">
        <span>User Age:</span> 
        <input
          class="user_age"
          type="number"
          v-model="user.age"
          />
      </div>
      <div class="users_info">
        <span>Is Active:</span>
        <input
          type="checkbox"
          v-model="user.isActive"
        />
      </div>
      <div class="action">
        <Btn type="success" @click="updateUser(user)">Update</Btn>
        <Btn type="danger" @click="deleteUser(user)">Delete</Btn>
      </div>
    </li>
  </ul>
</div>
</template>

<script setup>
import Btn from './Btn.vue'

const emits = defineEmits(['updateUser', 'deleteUser'])
const props = defineProps(['users'])

function isValidFields(user) {
  return user.name.length && user.age ? true : false
}
function updateUser(user) {
  if (!isValidFields(user)) return alert('Please fill all fields')
  emits('updateUser', user)
}
function deleteUser(user) {
  emits('deleteUser', user.docId)
}
</script>

<style scoped>
.users-list {
  padding: 0;
  margin: 0;
  list-style: none;
}
.users{
  border: 1px solid #ccc;
  padding: 20px;
  margin: 10px;
  list-style: none;
  width: 300px;
}
.users_info{
  display: flex;
  margin-top: 10px;
}
.user_name, .user_age{
  margin-left: 10px;
  border: none;
  border-bottom: 1px dashed #ccc;
}
.action{
  display: flex;
  gap: 10px;
}
</style>