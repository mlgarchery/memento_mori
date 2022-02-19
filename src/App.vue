<template>
  <div id="app">
    <div id="setup">
      <div>
        <h2 class="title">
          Your life<br/>
        </h2>
        <input v-model="myYear" placeholder="années" /> years <br>
        <input v-model="myMonth" placeholder="mois" /> monthes.
        <p> You've used {{parseInt(completedMonthes/(90*12) * 100)}} % of a 90-years, <br>
        fully creative and beautiful life. <br/>
        You'll be remembered.</p>
        <p>Just get to work.</p>
        <p>And clean your room.</p>
      </div>
    </div>
    <div id="life">
      <div 
        v-for="month in monthes"
        :key="month"
        @click="complete(month)"
        :class="['month', {['year']: month%120==0}, {['completedMonthes']: month <= completedMonthes}]" >
      {{parseInt(month/12)}} <br> {{month%12}}
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'App',
  mounted(){
    // load your age saved in the localStorage of your browser
    let myYear = localStorage.getItem("myYear");
    let myMonth = localStorage.getItem("myMonth");
    if(myYear) this.myYear = myYear;
    if(myMonth) this.myMonth = myMonth;
  },
  computed: {
    completedMonthes: {
      get(){
        return parseInt(this.myYear)*12 + parseInt(this.myMonth);
      },
      set(month){
        this.myYear = parseInt(month / 12);
        this.myMonth = parseInt(month % 12);
        this.setAgeInLocalStorage(this.myYear, this.myMonth);
      }
    }
  },
  data(){
    return {
      myYear: 27, // a default value
      myMonth: 11, // a default value
      monthes: Array.from(Array(90*12).keys()),
    }
  },
  methods: {
    complete(month){
      this.completedMonthes = month;
    },
    setAgeInLocalStorage(year, month){
      localStorage.setItem("myYear", year);
      localStorage.setItem("myMonth", month);
    }
  }
}
</script>

<style lang="scss">
$page_padding: 20px;
$square_size: 25px;
$font_size: 10px;
$square_margin: 4px;
$number_of_square_on_a_row: 42; // max number of month on a row
$app_width: $number_of_square_on_a_row * ($square_size + 2 * $square_margin);

#app{
  display: flex;
}

#setup{
  display: flex;
  width: 350px;
  align-items: center;
  justify-content: center;
  font-family: Arial;

  input{
    margin: 2px;
    width: 50px;
    border: 1px solid black;
  }
}

#life {
  display: flex;
  flex-flow: row wrap;
  width: $app_width;
  padding: 0;
}
.month{
  display: flex;
  align-items: center;
  justify-content: center;
  width: $square_size;
  height: $square_size;
  margin: $square_margin;
  font-size: $font_size;
  background-color: white;
  box-sizing: border-box;
  border: 1px solid black;
}

.year {
  border: 2px solid black;
}

.completedMonthes{
  background-color: rgb(0, 0, 0);
}
</style>
