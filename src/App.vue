<template>
  <div>
    <div v-if="activated">
      <h2>Это капитал-шоу - Поле чудес</h2>
      <hr/>
      <button @click='activated=false'>нажми чтоб играть</button>
    </div>
    <register v-else-if="!activated"></register>
  </div>
</template>

<script>

import register from './components/register.vue'

export default {
  name: 'App',
  data() {
    return {
      activated: true,
    }
  },
  methods: {

  },
  
  components: {
    register
  }
}
</script>

<style>
html {
  min-height: 100%;
}
body {
  background: no-repeat center center url('http://vyatkawalks.ru/upload/medialibrary/186/18691357840864be5133aa523831ebc2.jpg');
  background-size: 100%;
  font-family: cursive, sans-serif;
  color: #8a8a8a;
}
#app {
  box-shadow: 0px 0px 5px 5px rgba(117,117,117,0.75);
  background-color: rgb(225, 202, 202);
  border-radius: 20px;
  padding: 10px 30px;
  width: 100%;
  max-width: 1000px;
  margin: 4vh auto;
}
h2 {
  text-align: center
}
button {
  border: 3px;
  padding: 3px 5px;
  background-color: rgb(196, 95, 179);
  border-color: aqua;
  border-radius: 5px;
  font-family: cursive, sans-serif;
  display:block;
  margin:0 auto;
}
input[type="text"]{
  max-width: 300px;
  height: 25px;
  padding: 4px 10px;
  border: none;
  border-radius: 5px;
  font-family: cursive, sans-serif;
  color: #8a8a8a;
  display:block;
  margin:0 auto;
}

</style>
