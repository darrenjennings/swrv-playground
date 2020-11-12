<template>
  <div id="app">
    {{ data.results.map(p => p.name) }}
  </div>
</template>

<script lang="ts">
import { defineComponent } from '@vue/composition-api'
import useSwrv from 'swrv'
import HelloWorld from './components/HelloWorld.vue'

interface ApiResponse {
  results: Pokemon[]
}

interface Pokemon {
  name: string,
  url: string
}

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld
  },
  setup () {
    const { data } = useSwrv<ApiResponse>('key', () => {
      return fetch('https://pokeapi.co/api/v2/pokemon')
        .then(res => res.json())
        .then(json => json)
    })
    
    return {
      data
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
