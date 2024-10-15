<script setup>
import { ref, defineModel } from 'vue';

const email = ref("") // bây giờ thay vì dùng biến ref để thay đổi giá trị \
const email1 = defineModel('email');// truyền tên đối số vào hàm định nghĩa
const setEmailDefault = () =>
{
    email1.value = "lenguyen.@gmail.com"
}

const [username, modifiers] = defineModel('username', {
    set(value){
        if(modifiers.capitalize)
    {
        return value.charAt(0).toUpperCase() + value.slice(1);
    }
    return value
    }
});// truyền tên đối số vào hàm định nghĩa
console.log (modifiers)
const setUsernameDefault = () =>
{
    username.value = "lenguyen"
}


</script>
<template>
    <div>
        <label for="email1">Email</label>
        <input type="text" v-model="email1">
        <p>{{ email1 }}</p>
        <button @click="setEmailDefault"> Set email default</button>

        <label for="username">username</label>
        <input type="text" v-model="username">
        <p>{{ username }}</p>
        <button @click="setUsernameDefault"> Set username default</button>
    </div>
</template>