<script setup>
import { useRouter } from "vue-router";
import { ref } from "vue";
import Swal from "sweetalert2";



const name = ref("");
const professional_id = ref("");
const password = ref("");
const passwordcheck = ref("");

const registernurse = async (name, professional_id , password) => {
  // if (confirm("Please check you password") == true) {
  const res = await fetch(`${import.meta.env.VITE_BASE_URL}api/nurse/register`, {
    method: "POST",
    headers: {
      "content-type": "application/json",
    },
    body: JSON.stringify({
      name: name,
      professional_id: professional_id,
      password: password,
    }),
  });
  if (res.status === 200) {
    Swal.fire("คุณสร้างบัญชีสำเร็จ!");
    setTimeout(function () {
      close();
    }, 1500);
    console.log("You add user success");
  } else {
    console.log("error,cannot add");
    Swal.fire({
      icon: "error",
      title: "ขอโทษ !!!",
      text: "ไม่สามารถสร้างบัญชีได้ โปรดตรวจสอบความถูกต้อง!",
    });
  }
  
};

const checkmatch = () => {
  const pass = password;
  const passcheck = passwordcheck;
  if (pass.value === passcheck.value) {
    document.getElementById("password").style.backgroundColor = "#e9f7e3";
    document.getElementById("passwordcheck").style.backgroundColor = "#e9f7e3";
  }
  else {
    document.getElementById("password").style.backgroundColor = "#fae2e0";
    document.getElementById("passwordcheck").style.backgroundColor = "#fae2e0";
  }
};

const checkinputpassword = (pass,passcheck) => {
  if (pass.length === 0) {
    password.value = null;
    alert("โปรดใส่รหัสผ่าน")
  }
  if (pass.length < 8) {
    password.value = null;
    alert("รหัสผ่านต้องมีความยาวมากกว่า 8 ตัวอักษร")
  }
  if (passcheck != pass){
    password.value = null;
    alert("รหัสผ่านไม่ตรงกัน");
  }
};

const appRouter = useRouter();
const close = () => appRouter.push({ name: "home" });

</script>
 
<template>
 <div class="container mx-auto">
  <div class="flex flex-col items-center justify-center px-6 py-8 mx-auto md:h-screen lg:py-0">
      <div class="w-full rounded-lg shadow dark:border md:mt-0 sm:max-w-md xl:p-0 bg-white">
        <div class="p-6 space-y-4 md:space-y-6 sm:p-8">
              <h1  class="text-xl font-bold text-center leading-tight tracking-tight text-gray-900 md:text-2xl">
                ลงทะเบียนสำหรับพยาบาล
              </h1>
              <form class="space-y-4 md:space-y-6" >
                  <div>
                      <label 
                      class="block mb-2 text-sm font-medium text-gray-900">ชื่อผู้ใช้งาน
                      &nbsp;
                      <span style="font-size: 10px; color: rgb(177, 109, 241)">
                      ( ตัวอักษรต้องไม่เกิน 100 ตัวอักษร )
                      </span>
                      </label>
                      <input 
                      type="text"
                      class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:placeholder-gray-400 dark:focus:ring-blue-500 dark:focus:border-blue-500"
                      placeholder="xxxxxxxxxx" 
                      v-model.trim="name"
                      maxlength="100"
                      >
                       <p v-if="name.length" class="input-count">
                      {{ name.length }}/100
                      </p>
                       <p v-show="name.length < 1" >
                      * Please input your name <span></span>
               </p>
               <p v-show="name.length > 100" >
                * Characters must not exceed 100
              </p>

                  </div>

                  

                  <div>
                      <label 
                      class="block mb-2 text-sm font-medium text-gray-900">เลขใบประกอบวิชาชีพ</label>
                      <input 
                      v-model="professional_id"
                      placeholder="xxxxxxxx" 
                      maxlength="11"
                      class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:placeholder-gray-400 dark:focus:ring-blue-500 dark:focus:border-blue-500"
                      >
                       <p v-if="professional_id.length" class="input-count">
                      {{ professional_id.length }}/11
                      </p>
                       <p v-show="professional_id.length < 1" >
                      * Please input your professional_id  <span></span>
               </p>
               <p v-show="professional_id.length > 100" >
                * Characters must not exceed 11
              </p>
                  </div>

                  <div>
                      <label  
                      class="block mb-2 text-sm font-medium text-gray-900">รหัสผ่าน</label>
                      <input 
                      placeholder="xxxxxxxx" 
                      class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:placeholder-gray-400 dark:focus:ring-blue-500 dark:focus:border-blue-500"
                      type="password"
                      name="password"
                      v-model="password"
                      maxlength="14"
                      minlength="8"
                      >
                      <p v-if="password" class="input-count" id="count">
              {{ password.length }}/14
            </p>

            <p v-show="password.length < 8" id="checkname">
              * Password must not be less than 8 characters
            </p>
            <p v-show="password.length > 14" id="checkname">
              * Password must not be more than 14 characters
            </p>
                  </div>


                  <div v-show="password.length >= 1">
                      <label 
                      class="block mb-2 text-sm font-medium text-gray-900">ยืยยันรหัสผ่าน</label>
                      <input 
                      placeholder="xxxxxxxx" 
                      class="bg-gray-50 border border-gray-300 text-gray-900 sm:text-sm rounded-lg focus:ring-primary-600 focus:border-primary-600 block w-full p-2.5 dark:placeholder-gray-400 dark:focus:ring-blue-500 dark:focus:border-blue-500"
                      type="password"
                      name="passwordcheck"
                      v-model="passwordcheck"
                      maxlength="14"
                      minlength="8"
                      v-on:keyup="checkmatch"
                      >
                       <p v-if="passwordcheck" class="input-count" id="count">
                     {{ passwordcheck.length }}/14
                      </p>

                   <p v-show="passwordcheck.length < 8" id="checkname">
                   * Password must not be less than 8  characters
                    </p>
                   <p v-show="passwordcheck.length > 14" id="checkname">
                   * Password must not be more than 14 characters
                   </p>
                  </div>

                



                  <button
                   class="block w-full bg-blue-900 hover:bg-blue-800 text-white font-bold py-2 px-4 mb-4 border rounded"
                    @click="registernurse (name, professional_id, password)"
                   >
                   
                 สร้างบัญชี
                  </button>
                  <div class="text-center">
              <router-link :to="{ name: 'loginNurse' }">
                <p class="text-sm font-medium text-gray-500">
                   คุณมีบัชีอยู่แล้ว? 
                  <a
                    class="font-bold text-primary-600 hover:underline text-indigo-800"
                    >เข้าสู่ระบบ ที่นี้</a
                  >
                </p>
              </router-link>
              </div>

              </form>
          </div>
      </div>
  </div>
</div>


</template>
 
<style>

</style>