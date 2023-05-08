<script>
import CalculatorComponent from './components/CalculatorComponent/CalculatorComponent.vue'
import PersonStarWars from './components/PersonStarWars/PersonStarWars.vue'

export default {
  name: 'App',
  components: {
    CalculatorComponent,
    PersonStarWars,
  }
}
</script>

<template>
  <div class="container">
    <CalculatorComponent />
    <PersonStarWars />
  </div>
</template>

<style>
body, h1, p, input, button, select {
  font-family: Inter, Arial, sans-serif;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.container {
  display: flex;
  flex-direction: column;
}
</style>
