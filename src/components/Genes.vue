<template>
    <ul :devikinData="devikinData" >
        <li class="li-header">
            <span class="subtitle is-size-4">Genes</span>
        </li>
        <li>
            <span class="title is-size-4">Mouth: </span>
            <span class="subtitle is-size-4">{{ hasDevikinData? this.mouth : '???' }}</span>
        </li>
        <li>
            <span class="title is-size-4">Eyes: </span>
            <span class="subtitle is-size-4">{{ hasDevikinData? this.eyes : '???' }}</span>
        </li>
        <li>
            <span class="title is-size-4">Ears: </span>
            <span class="subtitle is-size-4">{{ hasDevikinData? this.ears : '???' }}</span>
        </li>
        <li>
            <span class="title is-size-4">Hair: </span>
            <span class="subtitle is-size-4">{{ hasDevikinData? this.hair : '???' }}</span>
        </li>
        <li>
            <span class="title is-size-4">Horns: </span>
            <span class="subtitle is-size-4">{{ hasDevikinData? this.horns : '???' }}</span>
        </li>
    </ul>
</template>

<script>
export default {
  name: 'Genes',
  props: {
    devikinData: Object
  },
  data() {
      return {
        data: null,
        devikinGenes: ['Dominant', 'Co-Dominant', 'Recessive', 'Bonded', 'Unique'],
        parts: ['Mouth', 'Eyes', 'Ears', 'Hair', 'Horns'],
        mouth: null,
        eyes: null,
        ears: null,
        hair: null,
        horns: null
    }
  },
  watch: {
      'devikinData': function () {
          this.data = this.devikinData
          this.setDevikinGene()
      } 
  },
  methods: {
    setDevikinGene: function () {
        if (this.devikinData.Set) {
            this.mouth = this.devikinGenes[3]
            this.eyes = this.devikinGenes[3]
            this.ears = this.devikinGenes[3]
            this.hair = this.devikinGenes[3]
            this.horns = this.devikinGenes[3]
        } else {
            for (let index = 0; index < this.parts.length; index++) {
                if (this.parts[index] == 'Mouth') {
                    this.mouth = this.devikinGenes[this.devikinData.Mouth.Tag]
                } else if (this.parts[index] == 'Eyes') {
                    this.eyes = this.devikinGenes[this.devikinData.Eyes.Tag]
                } else if (this.parts[index] == 'Ears') {
                    this.ears = this.devikinGenes[this.devikinData.Ears.Tag]
                } else if (this.parts[index] == 'Hair') {
                    this.hair = this.devikinGenes[this.devikinData.Hair.Tag]
                } else if (this.parts[index] == 'Horns') {
                    this.horns = this.devikinGenes[this.devikinData.Horns.Tag]
                }
            }
        }
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
