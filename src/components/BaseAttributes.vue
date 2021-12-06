<template>
    <ul :devikinData="devikinData" >
        <li class="li-header">
            <span class="subtitle is-size-4">Base Attributes</span>
        </li>
        <li>
            <span class="title is-size-4">Vitality: </span>
            <span class="subtitle is-size-4">{{ hasDevikinData? devikinData.VitBase : '???' }}</span>
        </li>
        <li>
            <span class="title is-size-4">Power: </span>
            <span class="subtitle is-size-4">{{ hasDevikinData? devikinData.PowBase : '???' }}</span>
        </li>
        <li>
            <span class="title is-size-4">Fortitude: </span>
            <span class="subtitle is-size-4">{{ hasDevikinData? devikinData.ForBase : '???' }}</span>
        </li>
        <li>
            <span class="title is-size-4">Agility: </span>
            <span class="subtitle is-size-4">{{ hasDevikinData? devikinData.AgiBase : '???' }}</span>
        </li>
        <li>
            <span class="title is-size-4">Sanity: </span>
            <span class="subtitle is-size-4">{{ hasDevikinData? devikinData.SanBase : '???' }}</span>
        </li>
    </ul>
</template>

<script>
export default {
  name: 'BaseAttributes',
  props: {
    devikinData: Object
  },
  data() {
      return {
          data: null
      }
  },
  watch: {
      'devikinData': function () {
          this.data = this.devikinData
      }
  },
  computed: {
    hasDevikinData: function () {
        return this.data? true : false
    }
  }
}
</script>

<style scoped>

</style>
