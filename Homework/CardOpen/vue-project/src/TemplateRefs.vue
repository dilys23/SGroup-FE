<script setup>
import { onMounted, ref } from 'vue';

const inputRef = ref(null)
onMounted(() =>
{
    inputRef.value.focus();
})

// Refs trong V-for
const itemRefs = ref([])
</script>
<template>
    <div>
        <!-- Bây giờ muốn vào trang này thì sẽ focus vào sự kiện input luôn chứ ko cần phải nhấp chuột đến ô input  -->
        <h1>Template Refs</h1>
        <input type="text" name="" id="" ref="inputRef"> 
        <!-- Giúp khi vào trang thì sẽ focus ngay vào ô input  -->
    </div>
</template>