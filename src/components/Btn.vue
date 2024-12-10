<template>
<div>
  <button
    :class="type === 'btn' ? 'btn' : 'btn ' + props.type"
    @click="$emit('click')"
  >
    <slot></slot>
  </button>
</div>
</template>

<script setup>
import { defineEmits } from 'vue'

const emits = defineEmits(['click'])
const props = defineProps({
  type: {
    type: String,
    default: 'btn'
  }
})

</script>

<style scoped>
.btn{
  margin-top: 10px;
  padding: 5px 10px;
  background-color: #333;
  color: #fff;
  border: none;
  cursor: pointer;
}
.btn.danger{
  background-color: rgb(189, 33, 33);
}
.btn.success{
  background-color: rgb(43, 173, 43);
}
</style>