<template>
  <div id="app">
      <div 
        v-for="month in monthes"
        :key="month"
        :class="['month', {['year']: month%120==0}, {['completed']: month <= completed}]" >
      {{ month }}
      </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  computed: {
    monthes() {
      let result = [];
      // A 90 years old life, for the optimists
      for(let i=1; i <= 90*12; i++){
        result.push(i);
      }
      return result;
    },
    completed(){
      return 336;
    }      
  },
}
</script>

<style lang="scss">
$page_padding: 20px;
$square_size: 25px;
$font_size: 10px;
$square_margin: 4px;
$number_of_square_on_a_row: 36; // 3 ans
$app_width: $number_of_square_on_a_row * ($square_size + 2 * $square_margin);
body {
  display: flex;
  justify-content: center;
  margin: 0;
  padding: $page_padding;
}
#app {
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
.completed{
  background-color: rgb(0, 0, 0);
}
</style>
