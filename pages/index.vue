<template>
  <div class='container'>
    <div class="todos">
      <h1>Todos will go here</h1>
    </div>
    <div class="pomodoro">
      <div class="timer">
      <h1>Timer goes here</h1>
    </div>
    <div class="completions">
      <h1>Completions go here</h1>
    </div>
    </div>
    
  </div>
</template>

<script>
export default {
  name: 'IndexPage'
}
</script>
<style scoped>
.container {
  display: flex;
  flex-direction: row;
  width: 100%;
}
.todos {
  width: 40%;
  margin: 20px;
  background: grey;
  text-align: center;
  padding: 20px;
  font-size: 12px;
}
.pomodoro {
  display: flex;
  flex-direction: column;
  width: 100%;
}
.timer {
  background: grey;
  font-size: 12px;
  text-align: center;
  margin: 20px;
  padding: 20px;
}
.completions {
  background: grey;
  font-size: 12px;
  text-align: center;
  margin: 20px;
  padding: 20px;
}
</style>
