<template>
  <div id="app">
    <h1>THE BIG LEPOLLSKI</h1>
    <Vote />
  </div>
</template>

<script>
import Vote from './components/Vote';

export default {
  name: 'app',
  components: {
    Vote
  }
}
</script>

<style lang="scss">

//----------Scss variables

$font-stack-normal: 'Titillium Web', sans-serif;
$font-stack-header: 'Yeseva One', cursive;
$primary-color: rgb(255, 238, 219);
$button-color-yes: rgb(97, 201, 168);
$button-color-no: rgba(186, 59, 70, .7);
$background-color: rgb(237, 155, 64);

//-----------main styling

body {
    font-family: $font-stack-normal;
    font-size: 14px;
    line-height: 1.6;
    margin: 0px;
    padding: 0px;
    height: 100vh;
    background-color: $background-color;
  }
  h1 {
    font-size: 50px;
    text-align: center;
    margin: 10px 25px 10px 25px;
    letter-spacing: 4px;
  }
  h2 {
    font-size: 24px;
    text-align: center;
    letter-spacing: 4px;
    margin: 25px;
  }

//-------divs ---------

#container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    background: none;
    margin: 10px 25px;
}

#question-div,
#vote-div,
#results-div {
    background-color: white;
    height: 500px;
    width: 400px;
    border: none;
    margin: 30px 25px;
    border-radius: 4px;
    box-shadow: 1px 1px 12px 3px rgba(232,232,232,1);
    display: flex;
    flex-direction: column;
    text-align: center; 
}

//-------divs within divs --------

.header-div,
.question-div,
.option-div,
.button-div {
    width: 100%;
}

//------ buttons --------

.btn-primary {
  background-color: $button-color-yes;
  font-family: $font-stack-normal;
  border: none;
  border-radius: 3px;
  width: 90px;
  height: 35px;
  color: white;
  margin-top: 40px;
}

.btn-add {
  width: 35px;
  height: 35px;
  border: none;
  color: white;
  background-color: $button-color-yes;
  border-radius: 4px;
  img {
    height: 10px;
  }
}

.btn-remove {
  width: 35px;
  height: 35px;
  padding: 8px 12px;
  border: none;
  color: white;
  background-color: $button-color-no;
  border-radius: 4px;
}

// .btn-vote {
//   width: 300px;
//   height: 30px;
//   border: none;
//   background-color: white;
//   padding: 8px;
//   margin: 5px;
//   text-align: center;
//   border-radius: 4px;
//   box-shadow: 1px 1px 8px 1px rgba(232,232,232,1);
// }



</style>
