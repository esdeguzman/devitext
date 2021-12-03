<template>
  <div>
    <section class="hero is-link">
      <div class="hero-body">
        <p class="title">
          Devitext
        </p>
        <p class="subtitle">
          A text base fantool Devikin search for your quick NFT view.
        </p>
        <input type="text" class="input" placeholder="Type Devikin ID here" v-model="devikinId" id="devikinId">
        <button class="button mt-2" @click="search" :disabled="!hasInput">Search</button>
      </div>
    </section>
    <div class="container p-2 mb-5 mt-5">
      <div class="columns">
        <div class="column">
          <BasicInformation :devikinData="devikinData" />
        </div>
        <div class="column">
          <SpecialTraits :bus="bus" :devikinData="devikinData" />
        </div>
        <div class="column">
          <Genes :devikinData="devikinData" />
        </div>
        <div class="column">
          <Affinities :devikinData="devikinData" />
        </div>
        <div class="column">
          <BaseAttributes :devikinData="devikinData" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import BasicInformation from './components/BasicInformation.vue'
import SpecialTraits from './components/SpecialTraits.vue'
import Genes from './components/Genes.vue'
import Affinities from './components/Affinities.vue'
import BaseAttributes from './components/BaseAttributes.vue'
import Vue from '../node_modules/vue'

export default {
  name: 'App',
  components: {
    BasicInformation,
    SpecialTraits,
    Genes,
    Affinities,
    BaseAttributes
  },
  mounted() {
      this.resetSearch()
  },
  data() {
    return {
      devikinId: '',
      devikinData: {},
      perfectAffinities: null,
      bus: new Vue()
    }
  },
  methods: {
      search: function () {
          fetch('https://inventory.api.devikins.com/asset/' + this.devikinId) //727551 284275
            .then(response => {
                if (response.status >= 200 && response.status <= 299) {
                  return response.json();
                } else {
                  throw Error(response.statusText);
                }
            })
            .then(data => {
                this.resetSearch()
                this.devikinData = data
            })
            .catch((error) => {
                alert(error)
                this.resetSearch()
            })
      },
      resetSearch: function () {
          this.devikinId = null
          this.bus.$emit('search-reset')
          document.getElementById('devikinId').focus()
      }
  },
  computed: {
    hasInput: function () {
        return this.devikinId? true : false
    },
    hasDevikinData: function () {
      return this.devikinData.length? true : false
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-family: "Montserrat";
}

.li-header {
  border-bottom: 1px solid orange;
}
</style>
