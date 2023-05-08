<script>
import axios from 'axios';
export default {
  name: 'PersonStarWars',
  data() {
    return {
      person: {},
    };
  },
  methods: {
    async loadData() {
      try {
        const response = await axios.get('https://swapi.dev/api/people/1/');
        this.person = response.data;
        console.log(response.data)
      } catch (error) {
        console.log(error);
      }
    }
  },
}
</script>

<template>
  <div class="wrapper">
    <h1 class="list__title">StarWars character</h1>
    <button class="list__button" @click="loadData">Go!!!</button>
    <div v-for="(value, key) in person" :key="key">
      <div class="list__element">
        <p>{{ key[0].toUpperCase() + key.slice(1) }}:</p>
        <p>{{ value }}</p>
      </div>
    </div>
    <h1 class="list__title">May the force be with you</h1>
  </div>
</template>

<style lang="scss" scoped>
@import './PersonStarWars.scss';
</style>',
