 <script setup>
import { ref , reactive, computed} from 'vue';

   const count = ref("0");
   function increase() {
    count.value ++;
   }
   const book = reactive({name : 'Book1', chapters: []})
   const firstName = ref("Nguyễn Thị ")
   const lastName = ref("Lê");
   const fullName = computed ({
    get()
    {
        return firstName.value + ' ' + lastName.value
    },
    set(newValue)
    {
        [firstName.value ]

    }
   })
   const changeFullName = () =>{
    fullName.value = 'B'
   }

//    const fullName = computed(() => firstName.value + ' ' + lastName.value )
   const addChapter = () =>
   {
    console.log ('test hàm')
    book.chapters.push ('Chapter')
    console.log(book.chapters)
   }
   const isPulished = () => {
    return book.chapters.length > 0 ?'có' : 'Không'
   }
   const isPulishedComputed = computed(() => {
    return book.chapters.length > 0 ?'có' : 'Không'
   })
</script>
<template>
    <div>

        <p id="count"> Count : {{ count }}</p>
        <button @click="increase">Increase</button>
        <p id = "count " > Book name: {{ book.name }}</p>
        <!-- <p id="count">Đã xuất bản : {{ book.chapters.length > 0 ?'có' : 'Không' }}</p>  -->
        <!-- nếu dùng như này thì với các điều kiện phức tạp khác thì code sẽ dài 
         nên sẽ tạo 1 hàm -->
         <p id="count">Đã xuất bản : {{isPulished ()}}</p> 
         <p id="count">Đã xuất bản : {{isPulishedComputed}}</p> 


        <button @click="addChapter">Add Chapter</button>
        <p id="count"> FullName : {{ fullName }}</p>
        <button @click="cha">Add Chapter</button>

        
    </div>
</template>