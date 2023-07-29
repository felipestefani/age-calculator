<script setup>
import { ref } from "vue";

  const day= ref('')
  const month = ref('')
  const year = ref('')
  const dayError = ref('')
  const monthError = ref('')
  const yearError = ref('')
  const date = new Date()
  const exhibitDay = ref('--')
  const exhibitMonth = ref('--')
  const exhibitYear = ref('--')
  const validDate = ref(false)

  const checkDaySize = () => {
    day.value = day.value.replace(/\D/g, '')
    day.value.length >= 1 ? dayError.value = '' : '' 
    day.value.length  == 2 ? document.getElementById('month').focus() : ''
  }

  const checkMonthSize = () => {
    month.value = month.value.replace(/\D/g, '')
    month.value.length >= 1 ? monthError.value = '' : ''
    month.value.length == 2 ? document.getElementById('year').focus() : ''
  }

  const checkYearSize = () => {
    dayError.value == 'Must be a valid date' ? dayError.value = '' : '' 
    year.value = year.value.replace(/\D/g, '')
    year.value.length >= 1 ? yearError.value = '' : ''
  }

  const calculateAge = () => {
    validDate.value = false
    exhibitDay.value = '--'
    exhibitMonth.value = '--'
    exhibitYear.value = '--'

    day.value.length == 0 ? dayError.value = 'This field is required' : 
    parseInt(day.value) <= 0 || parseInt(day.value) > 31 ? dayError.value = 'Must be a valid day' : ''

    month.value.length == 0 ? monthError.value = 'This field is required' :
    parseInt(month.value) <= 0 || parseInt(month.value) > 12 ? monthError.value = 'Must be a valid month' : ''

    year.value.length == 0 ? yearError.value = 'This field is required' :
    parseInt(year.value) > date.getFullYear() ? yearError.value = 'Must be in the past' : ''

    if(parseInt(year.value) <= 0) {
      monthError.value = ''
      yearError.value = ''
      dayError.value = 'Must be a valid date'
    }

    const birth1 = new Date(year.value, month.value-1, day.value)
    const birth = `${year.value}-${month.value}-${day.value}`
    console.log(birth);
    
    if(birth1.getDate()!=day.value || birth1.getMonth()+1 != month.value || birth1.getFullYear() != year.value) {
      dayError.value = 'Must be a valid date'
    } else {
      validDate.value = true
      useAgeCalculator(birth)
    } 
  }

  const useAgeCalculator = birth => {
    const birthDate = new Date(birth);
    const currentDate = new Date();

    let yearsDiff = currentDate.getFullYear() - birthDate.getFullYear();
    const birthMonth = birthDate.getMonth();
    const currentMonth = currentDate.getMonth();
    const birthDay = birthDate.getDate()+1;
    const currentDay = currentDate.getDate();

    let monthsDiff = currentMonth - birthMonth;
    let daysDiff = currentDay - birthDay;
    console.log(currentDay);
    console.log(birthDay);

    if (daysDiff < 0) {
      monthsDiff -= 1;
      const prevMonthLastDay = new Date(currentDate.getFullYear(), currentMonth, 0).getDate();
      daysDiff = prevMonthLastDay - birthDay + currentDay;
    }

    if (monthsDiff < 0) {
      yearsDiff -= 1;
      monthsDiff += 12;
    }

    exhibitYear.value = yearsDiff
    exhibitMonth.value = monthsDiff
    exhibitDay.value = daysDiff

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
          <input :class="{error: dayError}" id="day" type="text" pattern="\d*" placeholder="DD" maxlength="2" v-model="day" @keyup="checkDaySize">
          <span class="validation" v-if="dayError">{{ dayError }}</span>
        </label>
      </div>
      <div class="month">
        <label for="month">
          <p class="label">Month</p>
          <input :class="{error: monthError}" id="month" type="text" placeholder="MM" maxlength="2" v-model="month" @keyup="checkMonthSize">
          <span class="validation" v-if="monthError">{{ monthError }}</span>
        </label>
      </div>    
      <div class="year">
        <label for="year">
          <p class="label year">Year</p>
          <input :class="{error: yearError}" id="year" type="text" placeholder="YYYY" maxlength="4" v-model="year" @keyup="checkYearSize">
          <span class="validation" v-if="yearError">{{ yearError }}</span>
        </label>
      </div>
    </div>  
    <div class="line">
      <div class="one_line"></div>
      <button><img src="./assets/images/icon-arrow.svg" alt="arrow icon"></button>
    </div>
  </form>
    <div class="display">
      <p><span>{{  exhibitYear }}</span>years</p>
      <p><span>{{ exhibitMonth }}</span>months</p>
      <p><span>{{ exhibitDay }}</span>days</p>
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