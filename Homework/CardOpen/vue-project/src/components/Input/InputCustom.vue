<script setup>
import {} from "vue"
const props = defineProps(["value"]);
const valueInput = ref(props.value);

function emitValue(event)
{
    valueInput.value = event.target
}
</script>
<template>

</template>
