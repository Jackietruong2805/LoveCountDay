<script setup>
import {ref} from "vue";
let day = ref("");
let month = ref("");
let year = ref("");
let limitMaxDate = new Date();
limitMaxDate = limitMaxDate.getFullYear() + "-" + (limitMaxDate.getMonth() + 1) + "-" + limitMaxDate.getDate();

const inputRef = ref("");
let startDate = '';
let isStarting = ref(true);
let isClick = ref(false);
const handleStart = ()=>{
  localStorage.setItem("startDate", inputRef.value.value);
  localStorage.setItem("isClick", true);
  startDate = inputRef.value.value;
  isStarting.value = false;
  isClick.value = true;
};

const handleInterVal = setInterval(()=>{
  if(localStorage.getItem('isClick')){
    startDate = localStorage.getItem("startDate");
    isStarting.value = false;
    isClick.value = true;
  }
  if(!isStarting.value){
    let now = new Date();
    const yearDivision = 365*24*60*60*1000;
    const monthDivision = 30*24*60*60*1000;
    const dayDivision = 24*60*60*1000;
    day.value = Math.floor((now.getTime() - +(new Date(startDate)).getTime())/dayDivision);
    month.value = Math.floor((now.getTime() - +(new Date(startDate)).getTime())/monthDivision);
    year.value = Math.floor((now.getTime() - +(new Date(startDate)).getTime())/yearDivision);
  }
  if(isClick.value){
    clearInterval(handleInterVal);
  }
}, 200);

// hanleButton
let dayMonthYear = ref({
  content: '',
  title: ''
});

const handleDate = (content, title)=>{
  dayMonthYear.value.content = content;
  dayMonthYear.value.title = title;
};

// handle Reset
const handleReset = ()=>{
  localStorage.removeItem("startDate");
  localStorage.removeItem("isClick");
  window.location.reload();
};

// upload image

</script>




<template>
    <div class="container set-time" v-if="isStarting">
            <section>
                <h1 class="title">Nhập vào Ngày bắt đầu yêu</h1>
                <div class="set-date">
                    <input ref="inputRef" class="timer-start" id="start" type="date" min="2021-12-31" :max="limitMaxDate">
                </div>
            </section>
            <section>
                <button @click="handleStart" class="start-button">Bắt đầu</button>
            </section>
    </div>
      <div class="container timer" v-else>
        <div class="timer-him">
          <div class="timer-image timer-imageLeft"></div>
          <span class="name name-hao">Anh Hào</span>
        </div>
        <div class="timer-counter">
          <div class="timer-borderOutside">
                <div class="timer-borderInside">
                    <span class="timer-content">{{dayMonthYear.content == day && dayMonthYear.title == 'day' 
                    ? day : dayMonthYear.content == month && dayMonthYear.title == 'month'
                    ? month : dayMonthYear.content == year && dayMonthYear.title == 'year' ? year : day}}</span>
                    <span class="timer-title">{{dayMonthYear.content == day && dayMonthYear.title == 'day' 
                    ? 'Ngày' : dayMonthYear.content == month && dayMonthYear.title == 'month'
                    ? 'Tháng' : dayMonthYear.content == year && dayMonthYear.title == 'year' ? 'Năm' : "Ngày"}}</span>
                </div>                
          </div>
          <div class="button">
              <button @touchend="handleDate(day, 'day')" @click="handleDate(day, 'day')" class="button-days">Days</button>
              <button @touchend="handleDate(month, 'month')" @click="handleDate(month, 'month')" class="button-months">Months</button>
              <button @touchend="handleDate(year, 'year')" @click="handleDate(year, 'year')" class="button-years">Years</button>
          </div>
          <div class="reset">
              <button @touchend="handleReset" @click="handleReset" class="button-reset">
                    Reset
              </button>
          </div>
        </div>
        <div class="timer-her">
          <div class="timer-image timer-imageRight"></div>
          <span class="name name-nhi">Em bé <i class="fa fa-heart"></i></span>
        </div>
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

.name{
  font-family: 'Love Ya Like A Sister', cursive;
  font-size: 30px;
  background-color: whitesmoke;
  padding: 10px;
  border-radius: 20px;
}
.name-hao{
  border: 3px solid greenyellow;
}
.name-nhi{
  border: 3px solid violet;
}

.name-nhi i{
  color: red;
}

.timer{
  width: 80%;
  height: 100%;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  font-size: 110px;
  font-weight: bold;
}
.reset{
  max-width: 320px;
  width: 320px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}
.button-reset{
  padding: 15px 25px;
  border-radius: 20px;
  border: none;
  opacity: 0.8;
  font-weight: bold;
  cursor: pointer;
  max-width: 95px;
  width: 95px;
  background-color: coral;
  text-align: center;
}
.button-reset:hover{
  background-color: wheat;
  color: coral;
  transform: scale(1.11);
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
}
.timer-counter{
  display: flex;
  flex-direction: column;
  margin-bottom: 100px;
}

.timer-him, .timer-her{
  display: flex;
  flex-direction: column;
  margin-top: 100px;
  gap: 40px 0;
}

.timer-image{
  width: 300px;
  height: 300px;
  border-radius: 50%;
  background-position: center;
  background-size: cover;
}
.timer-imageLeft{
  background-image: url('../../img/hao.jpg');
  border: 3px solid greenyellow;
}
.timer-imageRight{
  border: 3px solid violet;
  background-image: url('../../img/nhi.jpg');
}


.title{
  font-weight: bold;
  font-size: 40px;
  color: white;
  font-family: 'Unbounded', cursive;
  margin-bottom: 45px;
}

.set-date{
  max-width: 300px;
  width: 270px;
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
  gap: 0 20px;
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

.button{
  max-width: 320px;
  width: 320px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 25px 0;
}

.button > *{
  padding: 15px 25px;
  border-radius: 20px;
  border: none;
  opacity: 0.8;
  font-weight: bold;
  cursor: pointer;
  max-width: 95px;
  width: 95px;
  text-align: center;
}

.button .button-days{
  background-color: blueviolet;
  color: aliceblue;
}

.button .button-days:hover{
  background-color: pink;
  color: blueviolet;
  transform: scale(1.11);
}

.button .button-months{
  background-color: violet;
  color: blanchedalmond;
  text-align: center;
}
.button .button-months:hover{
  background-color: wheat;
  color: rgba(255, 0, 0, 0.823);
  transform: scale(1.11);
}

.button .button-years:hover{
  background-color: coral;
  color: white;
  transform: scale(1.11);
  box-shadow: rgba(149, 157, 165, 0.2) 0px 8px 24px;
}

.timer-borderOutside{
  width: 310px;
  height: 310px;
  border: 5px solid black;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
  margin-bottom: 50px;
  margin-top: 50px;
  padding: 10px;
}
.timer-borderInside{
  width: 280px;
  height: 280px;
  border: 5px solid black;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
  flex-direction: column;
  gap: 0 10px;
}

.timer-content{
  font-size: 110px;
}
.timer-title{
  font-size: 30px;
}

.custom-file-input::-webkit-file-upload-button {
  visibility: hidden;
  opacity: 0;
}
.custom-file-input.input-left::before {
  content: 'Select some files';
  display: inline-block;
  border: 3px solid #999;
  border-radius: 3px;
  padding: 5px 8px;
  outline: none;
  white-space: nowrap;
  cursor: pointer;
  font-weight: 700;
  font-size: 10pt;
  color: violet;
  margin-left: 70px;
}
.custom-file-input.input-right::before {
  content: 'Select some files';
  display: inline-block;
  border: 3px solid #999;
  border-radius: 3px;
  padding: 5px 8px;
  outline: none;
  white-space: nowrap;
  cursor: pointer;
  font-weight: 700;
  font-size: 10pt;
  color: greenyellow;
  margin-left: 70px;
}
.custom-file-input.input-left:hover::before {
  border-color: greenyellow;;
  color: violet;
}
.custom-file-input.input-right:hover::before {
  border-color: violet;
}
.custom-file-input:active::before {
  background: -webkit-linear-gradient(top, #e3e3e3, #f9f9f9);
}

input[type='file'] {
  color: transparent;
}

</style>