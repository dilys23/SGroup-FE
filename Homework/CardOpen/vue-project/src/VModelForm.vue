<script setup>
import { ref , reactive, computed} from 'vue';
const text = ref("hê lô");
const text1 = ref("hihi");
const textarea = ref("test")
const handleInput = (e) => {
   text.value = e.target.value
   // đây là cách đồng bộ 2 chiều bth của js, ở input thì có event là input , có giá trị target trỏ đến ô input và nhận giá trị khi nhập vào 
}
const check = ref(false)
const checkedNames = ref([])
const radioCheck = ref()
const selectCheck = ref()
const  selected = ref("")
const firstOptions = ref("first Options")
const secondOptions = ref("second Options")

// Ràng buộc giá trị trong v-model
</script>
<template>
    <div>
        <h1>Form Input Binding </h1>        
        <p>Input :  {{ text }}</p>
        <input type="text" :value="text" @input="handleInput">
        <br>
        <!-- vue js hỗ trợ công cụ rút gọn : v-model  -->
        <p> Input với v-model {{ text1 }}</p>
        <input v-model="text1">
        
         <p> text area : {{ textarea }}</p>
        <textarea v-model="textarea"></textarea>
      
        <p>Checkbox :  {{ selected}}</p>
        <input type="checkbox" v-model="selected" id="a" value="A" true-value="yes" false-value = "no">
        <label for="a">A</label>

          <p>Multiple Checkbox :  {{ checkedNames}}</p>
        <input type="checkbox" v-model="checkedNames" id="a" value="A">
        <label for="a">A</label>
        <input type="checkbox" v-model="checkedNames" id="b" value="B">
        <label for="b">B</label>
        <input type="checkbox" v-model="checkedNames" id="c" value="C">
        <label for="c">C</label>
        <input type="checkbox" v-model="checkedNames" id="d" :value="firstOptions">
        <label for="d">D</label>
        <input type="checkbox" v-model="checkedNames" id="e" :value="secondOptions">
        <label for="e">E</label>
        <p> Radio Box {{ radioCheck }}</p>
        <input type="radio" v-model="radioCheck" id="a" value="A">
        <label for="a">A</label>
        <input type="radio" v-model="radioCheck" id="b" value="B">
        <label for="b">B</label>

        <p> SelectCheck : {{ selectCheck }}</p>
        <select v-model="selectCheck">
            <option disabled value="" >Please select one</option>
            <option :value="{name : 'A'}">A</option>
            <option>B</option>
            <option>C</option>

        </select>
       

        

         
    </div>
</template>