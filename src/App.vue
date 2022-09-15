<template>
   <main class="flex justify-center items-center h-screen">
    <div class="w-[350px] h-[650px] rounded-md bg-black px-2">
       <nav class="flex justify-between bg-black px-2 py-1">
        <p class="text-white text-sm">{{time}}</p>
        <div class="flex space-x-2 items-center">
          <span class="material-symbols-outlined text-sm text-white">
network_cell
</span>
          <span class="material-symbols-outlined text-white text-sm">
network_wifi
</span>
          <span class="material-symbols-outlined text-white">
battery_full_alt
</span>
        </div>
       </nav>
       
       <!--Calculation-->
       <section class="relative top-32 pr-4 font-sans h-24 mt-2">
        <input type="text" v-model="userData" class="text-white text-xl text-right bg-black relative left-16" disabled/>
          <!-- <p class="text-white text-xl text-right operation">308 <i class="fa-solid fa-xmark text-[#e25089] text-sm"></i> 42</p> -->
          <p class="text-white text-5xl text-right result font-bold"></p>
        </section>
        <!--Symbols-->
        <section class="mt-28 rounded-t-md p-4 bg-[#2a2d37] font-sans font-bold flex flex-col space-y-4">
          <div class="flex justify-between">
            <button class="w-14 h-14 rounded-md bg-black text-[#40b1a1] text-xl" @click="getValue">AC</button>
            <button class="w-14 h-14 rounded-md bg-black text-[#40b1a1] text-xl" @click="getValue"><i class="fa-solid fa-delete-left"></i></button>
            <button class="w-14 h-14 rounded-md bg-black text-[#9dcec7] text-xl" @click="getValue"><i class="fa-solid fa-percent"></i></button>
            <button class="w-14 h-14 rounded-md bg-black text-[#e25089] text-xl" @click="getValue"><i class="fa-solid fa-divide"></i></button>
          </div>
          <div class="flex justify-between">
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue">7</button>
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue">8</button>
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue">9</button>
            <button class="w-14 h-14 rounded-md bg-black text-[#e25089] text-xl" @click="getValue"><i class="fa-solid fa-xmark"></i></button>
          </div>
          <div class="flex justify-between">
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue">4</button>
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue">5</button>
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue">6</button>
            <button class="w-14 h-14 rounded-md bg-black text-[#e25089] text-xl" @click="getValue"><i class="fa-solid fa-minus"></i></button>
          </div>
          <div class="flex justify-between">
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue">1</button>
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue">2</button>
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue">3</button>
            <button class="w-14 h-14 rounded-md bg-black text-[#e25089] text-xl" @click="getValue"><i class="fa-solid fa-plus"></i></button>
          </div>
          <div class="flex justify-between">
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue"><i class="fa-solid fa-repeat"></i></button>
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue">0</button>
            <button class="w-14 h-14 rounded-md bg-black text-white text-xl" @click="getValue">.</button>
            <button class="w-14 h-14 rounded-md bg-black text-[#e25089] text-xl" @click="getValue"><i class="fa-solid fa-equals"></i></button>
          </div>
        </section>
    </div>
   </main> 
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import moment from 'moment'
export default defineComponent({
  name: 'App',
  mounted() {
    setInterval(() => {
      this.getTime()
    }, 1000)
  },
  data() {
    return {
      time: moment().format('h:mm:ss a'),
      userData:''
    }
  },
  methods: {
    getTime() {
      this.time = moment().format('h:mm:ss a')
    },
    getValue(e: any) {
      if(parseInt(e.target.innerText)){
        this.userData += e.target.innerText  
      }
      if(e.target.innerText === 'AC'){
        this.userData = '';
        document.querySelector('.result')!.innerHTML = ''
      }
      if(e.target.innerText === '.'){
        this.userData += e.target.innerText
      }
      if(e.target.innerText === '0'){
        this.userData += e.target.innerText
      }
      if(e.target.classList.contains('fa-minus')){
        this.userData += '-';
      }
      if(e.target.classList.contains('fa-plus')){
        this.userData += '+';
      }
      if(e.target.classList.contains('fa-xmark')){
        this.userData += 'x';
      }
      if(e.target.classList.contains('fa-divide')){
        this.userData += '/';
      }
      if(e.target.classList.contains('fa-percent')){
        this.userData += '%';
      }
      if(e.target.classList.contains('fa-delete-left')){
        if(this.userData.length > 0){
          this.userData = this.userData.slice(0, -1)
        }
        }
      if(e.target.classList.contains('fa-equals')){
       // check if result includes the multiplication symbol
        if(this.userData.includes('x')){
          // replace the multiplication symbol with the multiplication sign
          this.userData = this.userData.replace('x', '*')
        }
        let result = eval(this.userData)
        if(result.toString().includes('.')){
          result = result.toFixed(2)
        }
        document.querySelector('.result')!.innerHTML = result
      }
    }
  },

});
</script>
