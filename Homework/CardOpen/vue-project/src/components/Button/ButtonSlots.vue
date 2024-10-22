<script setup>
import { computed, ref } from 'vue';

// Dữ liệu giả
const data = ref([
    { title: "1 ", content: "Content 1" },
    { title: "2 ", content: "Content 2" },
    { title: "3 ", content: "Content 3" },
    { title: "4 ", content: "Content 4" },
    { title: "5 ", content: "Content 5" },
    { title: "6 ", content: "Content 6" },
    { title: "7 ", content: "Content 7" },
    { title: "8 ", content: "Content 8" },
    { title: "9 ", content: "Content 9" },
    { title: "10 ", content: "Content 10" },
    { title: "11 ", content: "Content 11" },
    { title: "12 ", content: "Content 12" },
]);

// Các biến phân trang
const page = ref(1);
const itemsPerPage = 3;
const maxPageButtons = 3;

// Dữ liệu hiện tại dựa trên trang
const currentData = computed(() => {
    return data.value.filter((item) => item.title.includes(search.value))
        .slice((page.value - 1) * itemsPerPage, page.value * itemsPerPage);
});

// Tính tổng số trang
const totalPages = computed(() => Math.ceil(data.value.length / itemsPerPage));

// Tính startPage dựa trên trang hiện tại và giới hạn maxPageButtons
const startPage = computed(() => {
    let start = Math.max(1, page.value - Math.floor(maxPageButtons / 2));
    // Đảm bảo rằng endPage không vượt quá tổng số trang, và startPage cũng không vượt qua endPage
    if (start + maxPageButtons - 1 > totalPages.value) {
        start = Math.max(1, totalPages.value - maxPageButtons + 1);
    }
    return start;
});

// Tính endPage, không vượt quá tổng số trang
const endPage = computed(() => {
    return Math.min(totalPages.value, startPage.value + maxPageButtons - 1);
});
const backPrevious = () =>
{
    if (page.value > 1) {
        page.value--;
    }
}
const nextPage = () =>
{
    if (page.value < totalPages.value) {
        page.value++;
    }
}
// Biến tìm kiếm
const search = ref("");
</script>

<template>
  <div>
    <h3>Button component</h3>
    <input type="text" v-model="search" placeholder="Search" />
    <h3>{{ search }}</h3>
    <br />
    
  
    <slot name="body" :data="currentData"> Title </slot>
    
   
   <button @click="backPrevious" :disabled="page === 1"><<</button>
    <button
      v-for="p in endPage - startPage + 1"
      :key="p"
      @click="page = startPage + p - 1"
      :class="{ active: page === startPage + p - 1 }"
    >
      {{ startPage + p - 1 }}
    </button>

    <!-- Nút chuyển đến trang cuối -->
    <button @click="nextPage" :disabled="page === totalPages">
      >>
    </button>
  </div>
</template>
<style scoped>
button {
  margin: 0 5px;
  padding: 5px 10px;
  cursor: pointer;
  background-color: white;
  border: 1px solid #ccc;
  border-radius: 3px;
  transition: background-color 0.3s ease, color 0.3s ease;
}

button:hover {
  background-color: #007bff; /* Màu khi hover */
  color: white;
}

button.active {
  background-color: #007bff; /* Màu khi đang active */
  color: white;
  border-color: #0056b3;
}

button:disabled {
  background-color: #e9ecef;
  cursor: not-allowed;
  color: #6c757d;
}
</style>