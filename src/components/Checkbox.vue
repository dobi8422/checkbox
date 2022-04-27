<script setup>
import { ref, defineEmits } from 'vue'

const labelSide = ref(true)

const singleCheck = ref(false)
const singleEmit = () => {
  singleCheck.value = !singleCheck.value
  emit('singleCheck', singleCheck)
}

// 加入顏色可新增 (有內建名字的顏色)
const allColor = ref(['Teal', 'Orange', 'Red', 'Cyan'])// ['Blue', 'Black', 'Yellowgreen]
const multipleCheck = ref([])
const addData = item => {
  multipleCheck.value.indexOf(item) === -1
    ? multipleCheck.value.push(item)
    : multipleCheck.value.splice(multipleCheck.value.indexOf(item), 1)
  emit('multipleCheck', multipleCheck)
}

const emit = defineEmits({
  singleCheck: Boolean,
  multipleCheck: Object
})
emit('singleCheck', singleCheck)
emit('multipleCheck', multipleCheck)
</script>

<template>
  <div>
    <div>
      <button class="button_side" @click="labelSide=!labelSide">
        {{ labelSide ? 'Label on Right' : 'Label on Left'}}
      </button>
      <p :class="{'test':labelSide}">{{ labelSide ? 'Label on Right' : 'Label on Left'}}</p>
    </div>

    <div>
      <button :class="{'single-active':singleCheck}" @click="singleEmit">✓</button>
      <p>Did you eat lunch today?</p>
    </div>
    <p>The model data: <span>{{ singleCheck }}</span></p>

    <div>
      <div v-for="color in allColor" :key="color">
        <button
          :class="{'multiple_button':multipleCheck.indexOf(color)!==-1,}"
          :style="{background: multipleCheck.indexOf(color)===-1 ? 'white' : color}"
          @click="addData(color)">✓</button>
        <p>{{ color }}</p>
      </div>
      <!-- <div>
        <button :class="{'button_color_Orange':multipleCheck.indexOf('Orange')!==-1}" @click="addData('Orange')">✓</button>
        <p>Orange</p>
      </div>
      <div>
        <button :class="{'button_color_Red':multipleCheck.indexOf('Red')!==-1}" @click="addData('Red')">✓</button>
        <p>Red</p>
      </div>
      <div>
        <button :class="{'button_color_Cyan':multipleCheck.indexOf('Cyan')!==-1}" @click="addData('Cyan')">✓</button>
        <p>Cyan</p>
      </div> -->
    </div>
    <p>The model data: <span>{{ multipleCheck[0] ? multipleCheck : 'none' }}</span></p>
  </div>
</template>

<style scoped>
div {
  display: flex;
  flex-flow: row;
  margin: 2rem .5rem;
}
button {
  width: 1.8rem;
  height: 1.8rem;
  border-radius: 3px;
  font-size: 1.5rem;
  line-height: 28px;
  background: white;
  border: 1px solid black;
  color: white;
}
p {
  margin: .5rem;
}
span {
  font-weight: 600;
}

.test {
  order: -1;
}

.button_side {
  width: fit-content;
  color: black;
}

.single-active {
  background: #268fcc;
  border: 1px solid transparent;
  color: white;
}

.multiple_button {
  border: 1px solid transparent;
  color: white;
}
.button_color_Teal {
  background: teal;
}
.button_color_Orange {
  background: orange;
}
.button_color_Red {
  background: Red;
}
.button_color_Cyan {
  background: cyan;
}
</style>
