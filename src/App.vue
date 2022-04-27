<script setup>
import { ref } from 'vue'
import Checkbox from './components/Checkbox.vue'

const emit = ref([])
const singleCheck = singleCheck => {
  emit.value[0] = singleCheck.value
}

const multipleCheck = multipleCheck => {
  emit.value[1] = multipleCheck.value
}
</script>

<template>
  <div>
    <Checkbox id="checkbox"
      @singleCheck=singleCheck
      @multipleCheck=multipleCheck />
    <div class="emit_box">
      emit: <br>
      1.{{ emit[0] }}<br>
      2.{{ emit[1] }}
    </div>
  </div>
</template>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}

#checkbox {
  display: flex;
  flex-flow: column;
  align-items: center;
  justify-content: center;
  height: 50vh;
}
</style>
