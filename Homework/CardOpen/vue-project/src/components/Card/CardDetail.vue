<script setup>
    import {ref} from "vue"
    import {defineProps, defineEmits,provide } from "vue"
    import Avatar from "../Avatar/Avatar.vue";
    const props = defineProps({
        cardProp: Object,
        imgLink: String,
    });
    provide('hello', "heloo");
    const khoai = defineEmits(["closePopup", "saveCard", "updateAvatar"])
    // console.log(cardProp.title)
    
    function save() {
        console.log("save đc gọi")
        khoai("saveCard", { id: "id-123", title: "Card 1", description: "Description 1" });
}
function updateAvatar() {
  khoai("updateAvatar");  // Phát sự kiện updateAvatar
}
</script>
<template>
   <div class="container">
    <h1 class="heading-1">
        Card Detail
    </h1>
    <div :class="card">
        <div class="card_image">
            <img src="" alt="">
        </div>
        <div class="card_content">
            <div>{{ cardProp }}</div>
            <h1 class="heading-2">{{ cardProp.title }}</h1>
            <p class="paragraph">{{ cardProp.description }}</p>
        </div>
    </div>
    <button @click = "$emit('closePopup')">Cancel</button>
    <button @click = "save">Save</button>
    <button @click = "updateAvatar">Update</button>
   </div>
</template>
<style>
</style>