<script setup>
import { ref, provide, watchEffect } from 'vue';
import CardDetail from './components/Card/CardDetail.vue';
import ButtonSlots from './components/Button/ButtonSlots.vue';
import Avatar from './components/Avatar/Avatar.vue';
import Computed from './Computed.vue';
import VModelForm from './VModelForm.vue';
import TemplateRefs from './TemplateRefs.vue';
import ComponentVModel from './ComponentVModel.vue';
import ButtonSlot from './components/Button/Slot.vue';
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
// Đối số trong Component-V-Model 
// có thể sử dụng nhiều đối số để binding trong component con 
const email1 = ref("")
const username = ref("")
watchEffect(() =>
{
  console.log(email1.value)
})
const changeEmailDefaultFromParent = () =>
{
  email1.value = "dilysnguyen@gmail.com   "
}
watchEffect(() =>
{
  console.log(email1.value)
})
const changeUsernameDefaultFromParent = () =>
{
  username.value = "dilysnguyen   "
}
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
  

  <div>
    <h3>Table Product</h3>
    <ButtonSlots>
    <template  #body="props">
      <template v-for="(item,index) in props.data" :key="index">
        <a>{{ item.title }}</a>
				<p>{{ item.content }}</p>

      </template> </template>
  </ButtonSlots>
  </div>
  <Computed/>
  <VModelForm/>
  <TemplateRefs/>
  <ButtonSlot>
    <template #save>Save</template>
    <template #delete>Delete</template>
    <template #update>Update</template>
  </ButtonSlot>
  <!-- <ComponentVModel v-model:email="email1"  v-model:username="username"/> -->
   <!-- Thực hiện modifier cho component vmodel  -->
  <ComponentVModel v-model:email="email1"  v-model:username.capitalize="username"/>

  <button @click="changeEmailDefaultFromParent">Change email</button>
  <button @click="changeUsernameDefaultFromParent">Change username</button>
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
