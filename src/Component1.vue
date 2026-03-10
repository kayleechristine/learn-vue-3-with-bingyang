<template>
  <div style="background-color: aqua; padding: 10px; margin: 20px">
    <h2>This is the Component1 component.</h2>
  </div>
</template>

<script setup>
import {
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted
} from 'vue'

console.log('Setup Component1.')

onBeforeMount(() => {
  console.log('Component1 is Before Mount.')
})
onMounted(() => {
  console.log('Component1 is Mounted.')
})
onBeforeUpdate(() => {
  console.log('Component1 is Before Update.')
})
onUpdated(() => {
  console.log('Component1 is Updated.')
})
onBeforeUnmount(() => {
  console.log('Component1 is Before Unmount.')
})
onUnmounted(() => {
  console.log('Component1 is Unmounted.')
})
</script>