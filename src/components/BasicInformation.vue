<template>
  <ul :devikinData="devikinData">
    <li class="li-header">
        <span class="subtitle is-size-4">Basic Information</span>
    </li>
    <li>
        <span class="title is-size-4">Devikin ID: </span>
        <span class="subtitle is-size-4">{{ devikinBasicInformation.id? devikinBasicInformation.id : '???' }}</span>
    </li>
    <li>
        <span class="title is-size-4">Overall Affinity: </span>
        <span class="subtitle is-size-4">{{ devikinBasicInformation.overallAffinity? devikinBasicInformation.overallAffinity : '???' }}</span>
    </li>
    <li>
        <span class="title is-size-4">Rarity: </span>
        <span class="subtitle is-size-4">{{ devikinBasicInformation.rarity? devikinBasicInformation.rarity : '???' }}</span>
    </li>
    <li>
        <span class="title is-size-4">Personality: </span>
        <span class="subtitle is-size-4">{{ devikinBasicInformation.personality? devikinBasicInformation.personality : '???' }}</span>
    </li>
    <li>
        <span class="title is-size-4">Ancestry: </span>
        <span class="subtitle is-size-4">{{ devikinBasicInformation.ancestry? devikinBasicInformation.ancestry : '???' }}</span>
    </li>
    <li>
        <span class="title is-size-4">Life Stage: </span>
        <span class="subtitle is-size-4">{{ devikinBasicInformation.lifeStage? devikinBasicInformation.lifeStage : '???' }}</span>
    </li>
    <li class="pt-2" v-if="devikinBasicInformation.id">
       <a :href="nftLink" class="button is-link is-uppercase has-text-weight-bold" target="_blank">view nft at klevernft.com</a>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'BasicInformation',
  props: {
    devikinData: Object
  },
  watch: {
      'devikinData': function () {
          this.setDevikinRarity()
          this.setDevikinPersonality()
          this.setDevikinAncestry()
          this.setDevikinLifeStage()
          this.devikinBasicInformation.overallAffinity = this.devikinData.OverallAffinity
          this.devikinBasicInformation.id = this.devikinData.SequenceCounter? this.devikinData.SequenceCounter : '0'
          this.nftLink = 'https://klevernft.com/asset/' + this.devikinBasicInformation.id
      } 
  },
  data() {
    return {
      devikinBasicInformation: {
          id: null,
          overallAffinity: null,
          rarity: null,
          personality: null,
          ancestry: null,
          lifeStage: null,
          nftLink: null
      },
      personalities: [
          {name: 'Angry', bonus: '+1 Power, +1 Agility'},
          {name: 'Curious', bonus: '+1 Agility, +1 Sanity'},
          {name: 'Feisty', bonus: '+2 Power'},
          {name: 'Nerdy', bonus: '+2 Fortitude'},
          {name: 'Polite', bonus: '+1 Vitality, +1 Fortitude'},
          {name: 'Reckless', bonus: '+1 Fortitude, +1 Sanity'},
          {name: 'Resilient', bonus: '+1 Vitality, +1 Power'},
          {name: 'Sassy', bonus: '+2 Agility'},
          {name: 'Shy', bonus: '+2 Vitality'},
          {name: 'Stoic', bonus: '+2 Sanity'},
          {name: 'Klever', bonus: '+1 all affinities'},
          {name: 'Lavish', bonus: '+2 Vitality, +1 Fortitude'},
          {name: 'Miner', bonus: '+2 Power, +1 Agility'},
          {name: 'Glitched', bonus: '+3 Sanity'},
      ]
    }
  },
  methods: {
    setDevikinRarity: function () {
        let overallAffinity = this.devikinData.OverallAffinity

        if (overallAffinity <= 29) {
            this.devikinBasicInformation.rarity = 'Common'
        } else if (overallAffinity >= 30 && overallAffinity <= 34) {
            this.devikinBasicInformation.rarity = 'Uncommon'
        } else if (overallAffinity >= 35 && overallAffinity <= 40) {
            this.devikinBasicInformation.rarity = 'Rare'
        } else if (overallAffinity >= 41 && overallAffinity <= 49) {
            this.devikinBasicInformation.rarity = 'Mythic'
        } else if (overallAffinity == 50) {
            this.devikinBasicInformation.rarity = 'Eldritch'
        }
    },
    setDevikinPersonality: function () {
        let personality = this.devikinData.Personality
        personality == 0? personality = 0 : personality -= 1

        for (let index = 0; index < this.personalities.length; index++) {
            if (index == personality) {
                this.devikinBasicInformation.personality = this.personalities[index].name + ' (' + this.personalities[index].bonus + ')'
                break
            }
        }
    },
    setDevikinAncestry: function () {
        let ancestry = this.devikinData.AncestryType

        switch (ancestry) {
            case 1:
                this.devikinBasicInformation.ancestry = 'Lunarian'
                break;
            case 2:
                this.devikinBasicInformation.ancestry = 'Ochran'
                break;
            case 3:
                this.devikinBasicInformation.ancestry = 'Glyesian'
                break;
            case 4:
                this.devikinBasicInformation.ancestry = 'Maarish'
                break;
            case 5:
                this.devikinBasicInformation.ancestry = 'Khoroth'
                break;

            default:
                break;
        }
    },
    setDevikinLifeStage: function () {
        let lifeStage = this.devikinData.Stage

        switch (lifeStage) {
            case 0:
                this.devikinBasicInformation.lifeStage = 'Embryo'
                break;
        
            default:
                break;
        }
    }
  }
}
</script>

<style scoped>

</style>
