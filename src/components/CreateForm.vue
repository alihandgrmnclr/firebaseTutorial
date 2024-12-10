<template>
<div  class="create_form">
  <h2>Add User</h2>
  <form class="form" @submit.prevent="addUser">
    <input
      class="create_name"
      v-model="userData.name"
      placeholder="Name"
    />
    <input
      class="create_age"
      v-model="userData.age"
      placeholder="Age"
      type="number"
      min="1"
    />
    <label>
      <input
        v-model="userData.isActive"
        type="checkbox"
      />
      <span>Is Active</span>
    </label>
    <Btn @click="handleClick">Add User</Btn>
  </form>
</div>
</template>

<script setup>
import { computed, ref } from 'vue'
//
import Btn from './Btn.vue'

const emits = defineEmits(['addUser'])
const userData = ref({
  name: '',
  age: 1,
  isActive: false,
  id: getRandomId()
})

const invalidFormData = computed(() => {
  return userData.value.name.length || userData.value.age < 1
})

function getRandomId() {
  return `userId-${Math.floor(Math.random() * 999_999_999)}`
}

function setDefaultData() {
  userData.value = {
    name: '',
    age: 1,
    isActive: false,
    id: getRandomId()
  }
}

function handleClick() {
  if (!invalidFormData.value) return alert('Please fill all fields')
  emits('addUser', userData.value)
  setDefaultData()
}
</script>

<style scoped>
.create_form {
  width: 300px;
  margin-top: 20px;
  padding: 20px;
  border: 1px solid #ccc;
}
.form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.create_name, .create_age {
  padding: 5px;
  border: none;
  border-bottom: 1px dashed #ccc;
}
</style>