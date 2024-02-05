<script setup>
import { useRouter } from "vue-router";
import { ref, onBeforeMount, computed, onMounted, onUnmounted } from "vue";
import Layout from '../layouts/Layout.vue';


const questions = ref([
  {
    text: 'คำถามที่ 1',
    options: ['ถูก', 'ผิด'],
    correctAnswer: 1,
  },
  {
    text: 'คำถามที่ 2',
    options: ['ถูก', 'ผิด'],
    correctAnswer: 1,
  },
  {
    text: 'คำถามที่ 3',
    options: ['ถูก', 'ผิด'],
    correctAnswer: 1,
  },
  {
    text: 'คำถามที่ 4',
    options: ['ถูก', 'ผิด'],
    correctAnswer: 1,
  },
  {
    text: 'คำถามที่ 5',
    options: ['ถูก', 'ผิด'],
    correctAnswer: 1,
  },
  {
    text: 'คำถามที่ 6',
    options: ['ถูก', 'ผิด'],
    correctAnswer: 1,
  },
  {
    text: 'คำถามที่ 7',
    options: ['ถูก', 'ผิด'],
    correctAnswer: 1,
  },
  {
    text: 'คำถามที่ 8',
    options: ['ถูก', 'ผิด'],
    correctAnswer: 1,
  },
  {
    text: 'คำถามที่ 9',
    options: ['ถูก', 'ผิด'],
    correctAnswer: 1,
  },
  {
    text: 'คำถามที่ 10',
    options: ['ถูก', 'ผิด'],
    correctAnswer: 1,
  },
  // เพิ่มคำถามต่อไปตามต้องการ
]);

// ตัวแปรเก็บคำตอบของผู้ใช้
const userAnswers = ref(Array(questions.value.length).fill(null));


// ตัวแปรเพื่อแสดงผลลัพธ์หลังจากทำการตรวจสอบคำตอบ
const showResults = ref(false);

// ฟังก์ชันเช็คคำตอบ
const checkAnswers = () => {
    console.log("checkAnswers is called");
    console.log(userAnswers);
   let correctCount = 0;

  // ตรวจสอบคำตอบของแต่ละคำถาม
  questions.value.forEach((question, index) => {
    console.log( question.correctAnswer, '-----------------', userAnswers.value[index] )
    if (userAnswers.value[index] === question.correctAnswer) {
        console.log('เข้าไหม')
      correctCount++;
    }
  });

  // อัพเดทผลลัพธ์และแสดงผล
  showResults.value = true;
  correctAnswers.value = correctCount;
  totalQuestions.value = questions.value.length;

  // หลังจากนั้นทำให้ปุ่มไม่สามารถกดได้
  submitClicked.value = true;
};

// disable ปุ่มส่งคำตอบหลังกดส่ง
const submitClicked = ref(false);

// ตัวแปรเก็บผลลัพธ์
const correctAnswers = ref(0);
const totalQuestions = ref(0);

console.log( userAnswers.value )
</script>
 


<template>
    <Layout class="bg-gradient-to-b from-blue-100">
        <div class="container mx-auto">
            <div
                class="box-content p-3 ml-5 mr-5 mt-10 bg-gradient-to-b from-blue-900 to-blue-800 shadow-lg shadow-slate-500/50 rounded-lg">
                <h2 class="font-semibold text-xl text-center text-slate-200">
                    สาระความรู้
                </h2>
            </div>

            <div
                class="box-content bg-white shadow-lg shadow-gray-300/50 mt-10 ml-5 mr-5 pt-6 pb-6 pl-20 pr-20 mb-10 rounded-lg">

                <p class="text-center font-bold text-lg">แบบทดสอบ</p>



                <!-- แสดงคำถามและตัวเลือก -->
    <div v-for="(question, index) in questions" :key="index">
      <p>{{ question.text }}</p>
      <div v-for="(option, optionIndex) in question.options" :key="optionIndex">
        <input
          type="radio"
          :id="`q${index}o${optionIndex}`"
          :name="`q${index}`"
          :value="optionIndex"
          v-model="userAnswers[index]"
        />
        <label :for="`q${index}o${optionIndex}`">{{ option }}</label>
      </div>
    </div>
<br>
    <!-- แสดงผลลัพธ์ -->
    <div v-if="showResults">
      <h2>ผลลัพธ์</h2>
      <p>คุณตอบถูก {{ correctAnswers }} ข้อจากทั้งหมด {{ totalQuestions }} ข้อ</p>
    </div>
    <br>
    <!-- ปุ่มส่งคำตอบ -->
    <button @click="checkAnswers" :class="{ 'hidden' : submitClicked }" class="block w-full bg-blue-900 hover:bg-blue-800 text-white font-bold py-2 px-4 border rounded text-center">ส่งคำตอบ</button>
    
    <router-link :to="{ name: 'knowledge' }"
    class="block w-full bg-blue-900 hover:bg-blue-800 text-white font-bold py-2 px-4  border rounded text-center">กลับ</router-link>
    
  </div>
    

        </div>


    </Layout>
</template>
 
<style></style>