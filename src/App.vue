<template>
  <div id="app" class="">
    <div class="notification is-danger">
      Show your favorite breeds of dog some love by selecting a breed from the dropdown
    </div>
    <div id="chart" ref="chart" v-show="breedLove.length">


    </div>
    <div class="columns">
      <div class="column"></div>
      <div class="column is-one">
        <api-select @change="change" label="Breeds" api="https://dog.ceo/api/breeds/list"></api-select>

        <figure>
          <p class="image">
            <api-image api="https://dog.ceo/api/breed/${id}/images/random" :id="id"></api-image>
          </p>
        </figure>
        <br>
        <nav class="level" v-if="id">
          <div class="level-item has-text-centered">
            <p class="control">
              <a class="button is-danger" @click="love">
          <span class="icon is-small">
            <i class="fa fa-heart"></i>
          </span>
                <span>Love</span>
              </a>
            </p>
          </div>
        </nav>
      </div>
      <div class="column"></div>
    </div>

  </div>
</template>

<script>
import apiSelect from './components/api-select.vue'
import apiImage from './components/api-image.vue'
import d3 from 'd3'
export default {
  components: {apiSelect, apiImage},
  name: 'app',
  data () {
    return {
      id: null,
      breedLove: []
    }
  },
  methods: {
    change (e) {
      this.id = e
    },
    love () {
      let breed = this.breedLove.find((item) => item.name === this.id)
      if(breed) {
        breed.value++
      } else {
        this.breedLove.push({name: this.id, value: 1})
      }
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
