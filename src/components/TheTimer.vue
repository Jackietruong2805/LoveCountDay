<script setup>
import {ref} from "vue";
let day = ref("");
let month = ref("");
let year = ref("");
let date = new Date();
date = date.getFullYear() + "-" + (date.getMonth() + 1) + "-" + date.getDate();

const inputRef = ref("");
let startDate = '';
let isStarting = ref(true);
const handleStart = ()=>{
  startDate = inputRef.value.value;
  isStarting.value = false;
};

setInterval(()=>{
  if(!isStarting.value){
    let now = new Date();
    year.value = +now.getFullYear() - +startDate.slice(0, 4);
    month.value = year.value*12 + +now.getMonth() + 1 - +startDate.slice(5, 7);
    let dayOver = 0;
    if(+now.getDay() < 12 && year.value > 0){
      dayOver = 7;
    }
    else if(+now.getMonth() < 11 && +now.getDate() == 30 && year.value > 0){
      dayOver = 7;
    }else if(+now.getMonth() < 9 && +now.getDate() == 30 && year.value > 0){
      dayOver = 6;
    }else if(+now.getMonth() < 6 && +now.getDate() == 30 && year.value > 0){
      dayOver = 5;
    }else if(+now.getMonth() < 4 && +now.getDate() == 30 && year.value > 0){
      dayOver = 4;
    }else if(+now.getMonth() < 2 && +now.getDate() == 28 && year.value > 0){
      dayOver = 3;
    }else{
      dayOver = 0;
    }
    day.value = year.value*365 + (+now.getMonth() + 1 - +startDate.slice(5, 7))*31 - dayOver + +now.getDate() - +startDate.slice(-2);
  }
  }, 1000);
</script>


<template>
    <div class="container set-time" v-if="isStarting">
            <section>
                <h1 class="title">Nhập vào Ngày bắt đầu yêu</h1>
                <div class="set-date">
                    <input ref="inputRef" class="timer-start" id="start" type="date" min="2021-12-31" :max="date">
                </div>
            </section>
            <section>
                <button ref="buttonRef" @click="handleStart" class="start-button">Bắt đầu</button>
            </section>
        </div>
        <div class="timer container" v-else>
            <span class="timer-item">{{day}}</span>
            <span>:</span>
            <span class="timer-item">{{month}}</span>
            <span>:</span>
            <span class="timer-item">{{year}}</span>
        </div>
</template>


<style scoped>
.set-time{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  height: 100%;
  gap: 30px 0;
}

.timer{
  max-width: 900px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 110px;
  font-weight: bold;
}

.title{
  font-weight: bold;
  font-size: 40px;
  color: white;
  font-family: 'Rubik Gemstones', cursive;
  margin-bottom: 45px;
}

.set-date{
  max-width: 300px;
  width: 250px;
  margin: 0 auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: bisque;
  border: 2px solid gray;
  border-radius: 20px;
  padding: 0 15px;
  gap: 0 20px;
  box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
}
.timer-start, .timer-start:focus{
  border: none;
  padding: 5px;
  background-color: transparent;
  font-size: 30px;
  color: blueviolet;
  outline: none;
  display: flex;
  gap: 0 10px;
}
input[type="date"]::-webkit-inner-spin-button,
input[type="date"]::-webkit-calendar-picker-indicator {
  font-size: 30px;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
}

.start-button, .start-button:hover{
  padding: 15px 30px;
  border-radius: 20px;
  border: none;
  background: green;
  color: white;
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
  cursor: pointer;
}

</style>