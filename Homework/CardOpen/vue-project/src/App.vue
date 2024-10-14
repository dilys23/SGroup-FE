<script setup>
import { ref, provide } from 'vue';
import CardDetail from './components/Card/CardDetail.vue';
import ButtonSlots from './components/Button/ButtonSlots.vue';
import Avatar from './components/Avatar/Avatar.vue';
const listCard = ref([
  {
    id: 1,
    title: "Card 1",
    description: "Description 1"
  },
  {
    id: 2,
    title: "Card 2",
    description: "Description 2"
  },
  {
    id: 3,
    title: "Card 3",
    description: "Description 3"
  }
]);
const CardDetailVisible = ref(false);
const selectedCard = ref(null)
function showDetail(item) {
  selectedCard.value = item;
  console.log(selectedCard.value)
  CardDetailVisible.value = true;

}
function closePopupDetail(...a) {
  console.log("close showDetail")
  CardDetailVisible.value = false;
  console.log(a);
}
function updateCard(value) {
  CardDetailVisible.value = true;
  const { id, ...body } = value;
  console.log(value);
  console.log(id);
  console.log(body);
}
function updateAvatar(){
  console.log("Update Avatar")
}
// Cập nhật link ảnh avatar
const imgLink = ref('https://lenguyen/2312');
// provide("imgLink", imgLink);
</script>

<template>
  <div class="container">
    <li v-for="item in listCard" :key="item.id" @click="showDetail(item)">
      <h2 class="heading-2"> {{ item.title }}</h2>
      <p class="paragraph"> {{ item.description }}</p>
    </li>
  </div>
  <CardDetail 
  v-if="CardDetailVisible" 
  :cardProp="selectedCard"
   @closePopup="closePopupDetail"
    @saveCard="updateCard" 
    :listCard="listCard"
    @updateAvatar = "updateAvatar"
    :imgLink="'https://lenguyen/2312'"/>
  <Avatar />
  <ButtonSlots>
    <template> #title</template>
  </ButtonSlots>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  border-radius: 10px;
  border: 1px solid #ccc;
  gap: 10px;
}

li {
  list-style-type: none;
  border: 1px solid #ccc;
  background-color: #ddd;
}
</style>
