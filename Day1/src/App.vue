<script setup>
import {ref, onMounted} from 'vue'
const count = ref(0)
function increment()
{
    count.value++
}
const dynamicId = ref(`div-${count.value}`);
onMounted(()=>
{
    console.log(`The initial count is ${count.value}`)
});
// function data() {
//   return {
//     article: '<p>Đây là một bài viết <strong>rất quan trọng</strong>.</p><p>Nội dung được định dạng bằng HTML.</p>'
//   }
// }
const objectOfAttrs = {
  id: 'container',
  class: 'wrapper',
  style: 'background-color:green'
}
 const checkboxValue = ref([]);
 function checkboxValue() {
  console.log(checkboxValue.value)
 }
 const radioValue = ref()
</script>
<template>
  <button @click="increment"> Count is : {{ count }}</button>
  <div v-bind:id="dynamicId">helo</div>
  <div v-bind="objectOfAttrs">Hi</div>
  la
  <div>
    {{ article }}
  </div>
  <div v-html="article"></div>
  <span>{{ checkboxValue }}</span>
  <input type="checkbox" value = "Lê" v-model="checkboxValue"/>
  <input type="checkbox" value = "Tiến Đạt" v-model="checkboxValue"/>
  <input type="checkbox" value = "Khoai" v-model="checkboxValue"/>


  <span>{{ radioValue }}</span>
  <input type="radio" value = "Lê" v-model="radioValue"/>
  <input type="radio" value = "Tiến Đạt" v-model="checkboxValue"/>
  <input type="radio" value = "Khoai" v-model="checkboxValue"/>

</template>
<style scoped>
 button{
    font-weight: bold;
 }
</style>