<script setup>
import { ref } from "vue";

  const day= ref('')
  const month = ref('')
  const year = ref('')
  const dayEmpty = ref(false)
  const monthEmpty = ref(false)
  const yearEmpty = ref(false)

  const checkDaySize = () => {
    day.value.length >= 1 ? dayEmpty.value = false : ''
    day.value.length == 2 ? document.getElementById('month').focus() : ''
  }

  const checkMonthSize = () => {
    month.value.length >= 1 ? monthEmpty.value = false : ''
    month.value.length == 2 ? document.getElementById('year').focus() : ''
  }

  const checkYearSize = () => {
    year.value.length >= 1 ? yearEmpty.value = false : ''
  }

  const calculateAge = () => {
    day.value.length == 0 ? dayEmpty.value = true : ''
    month.value.length == 0 ? monthEmpty.value = true : ''
    year.value.length == 0 ? yearEmpty.value = true : ''
  }

</script>

<template>
  <div class="teste">
  <div class="container">
    <form class="inputs" @submit.prevent="calculateAge">
      <div class="inputs">
      <div class="day">
        <label for="day">
          <p class="label">Day</p>
          <input :class="{error: dayEmpty}" id="day" type="text" placeholder="DD" maxlength="2" v-model="day" @keyup="checkDaySize">
          <span class="validation" v-if="dayEmpty">This field is required</span>
        </label>
      </div>
      <div class="month">
        <label for="month">
          <p class="label">Month</p>
          <input :class="{error: monthEmpty}" id="month" type="text" placeholder="MM" maxlength="2" v-model="month" @keyup="checkMonthSize">
          <span class="validation" v-if="monthEmpty">This field is required</span>
        </label>
      </div>    
      <div class="year">
        <label for="year">
          <p class="label year">Year</p>
          <input :class="{error: yearEmpty}" id="year" type="text" placeholder="YYYY" maxlength="4" v-model="year" @keyup="checkYearSize">
          <span class="validation" v-if="yearEmpty">This field is required</span>
        </label>
      </div>
    </div>  
    <div class="line">
      <div class="one_line"></div>
      <button><img src="./assets/images/icon-arrow.svg" alt="arrow icon"></button>
    </div>
  </form>
    <div class="display">
      <p><span>--</span>years</p>
      <p><span>--</span>months</p>
      <p><span>--</span>days</p>
    </div>
    <div class="attribution">
      Challenge by <a href="https://www.frontendmentor.io?ref=challenge" target="_blank">Frontend Mentor</a>. 
      Coded by <a href="#">Your Name Here</a>.
    </div>
  </div>
</div>
</template>

<style scoped>
.teste {
  width:100vw;
  display: flex;
  justify-content: center;
  align-items: center;
}
  .container {
    display: flex;
    flex-direction: column;
    background-color: var(--white);
    border-radius: 20px 20px 180px 20px;
    padding: 3em;
    max-width: 50em;
    width: 90%;
    max-height: 40em;
  }
  form{
    display: flex;
    flex-direction: column;
  }
  .inputs {
    display: flex;
  }
  .day, .month, .year {
    display: flex;
    flex-direction: column;
  }
  label {
    letter-spacing: 0.2em;
    color: var(--smokey-grey);
    font-weight: 700;
    font-style: normal;
    font-size: 16px;
    text-transform: uppercase;
    display: flex;
    flex-direction: column;
  }
  .label{
    font-size: 1em;
    color: var(--smokey-grey);
    font-style: normal;
    margin-bottom: 0.5em;
  }
  .year {
    margin-right: 10em;
  }
  input {
    font-size: var(--font-size);
    width: 4.5em;
    margin-top: 0.2em;
    margin-right: 1em;
    border: none;
    border: 1px solid var(--light-grey);
    border-radius: 5px;
    padding: 0.2em 0.8em;
    font-weight: 700;
  }
  .error{
    border: 1px solid var(--light-red);
  }
  .validation {
    color: var(--light-red);
    font-size: 11px;
    font-weight: 400;
    font-style: italic;
    text-transform: none;
  }
  ::placeholder{
    color: var(--smokey-grey);
  }
  .line{
    display: flex;
    align-items: center;
    width: 100%;
  }
  .one_line{
    border: 0.5px solid var(--light-grey);
    width: 100%;
  }
  button {
    border: none;
    background-color: transparent;
  }
  img {
    background-color: var(--purple);
    padding: 1.5em;
    border-radius: 100%;
  }
  p {
    color: var(--off-black);
    font-size: 6rem;
    font-weight: 800;
    font-style: italic;
    line-height: 1.1em;
  }
  span {
    color: var(--purple);
    letter-spacing: 0.1em;
  }
  .attribution { 
    font-size: 11px; 
    text-align: center; 
    position: absolute;
    bottom: 1em;
    left: 50%;
    transform: translate(-50%,0);
  }
  .attribution a {
    color: hsl(228, 45%, 44%); 
  }
  input:hover {
    cursor: pointer;
  }
  img:hover{
    cursor: pointer;
    background-color: var(--off-black);
  }
  input:focus{
    outline: none;
    border: 2px solid var(--purple-light);
    caret-color: var(--purple-light);
  }

  @media (max-width: 750px) {
    .container{
      width: 90%;
      padding: 3em 0em 2em 1.5em;
      border-radius: 15px 15px 80px 15px;
    }
    label{
      font-size: 12px;
    }
    .year {
      margin-right: 0.5em;
    }
    p{
      font-size: 3em;
    }
    input{
      /* margin: 0; */
      width: 5em;
      font-size: 1.4em;
      padding: 0.5em 1em;
    }
    .line{
      position: relative;
      margin: 3.5em 0;  
    }
    .one_line{
      align-items: center;
      justify-content: center;
      width: 100%;
      margin-right: 1.5em;
    }
    img{
      width: 4em;
      padding: 1em;
      position: absolute;
      left: 50%;
      transform: translate(-70%, 0);
    }
    .display{
      margin-top: 0.5em;
    }
  }
</style>