<template>
    <ul :bus="bus">
        <li class="li-header">
            <span class="subtitle is-size-4">Special Traits</span>
        </li>
        <li>
            <span class="title is-size-4">Perfect Affinities: </span>
            <span class="subtitle is-size-4">{{ perfectAffinities? perfectAffinities : '???' }}</span>
        </li>
        <li>
            <span class="title is-size-4">Bonded: </span>
            <span class="subtitle is-size-4">{{ bonded? bonded : '???' }}</span>
        </li>
        <li>
            <span class="title is-size-4">Is Hardminted: </span>
            <span class="subtitle is-size-4">{{ isHardminted? isHardminted : '???' }}</span>
        </li>
        <li>
            <span class="title is-size-4">Has Limited Hat: </span>
            <span class="subtitle is-size-4">{{ hasLimitedHat? hasLimitedHat : '???' }}</span>
        </li>
    </ul>
</template>

<script>
import Vue from '../../node_modules/vue'

export default {
  name: 'SpecialTraits',
  props: {
    devikinData: Object,
    bus: Vue
  },
  mounted() {
      this.bus.$on('search-reset', () => {
          this.resetSearch()
      })
  },
  watch: {
      'devikinData': function () {
          this.setPerfectAffinities()
          this.setDevikinBondedStatus()
          this.setDevikinHardmintStatus()
          this.setDevikinLimitedHat()
      } 
  },
  data() {
      return {
        perfectAffinities: null,
        bonded: null,
        isHardminted: null,
        hasLimitedHat: null,
        limitedHats: [
            {name: 'Mysth', description : 'Witch Hat'},
            {name: 'Scappy', description: 'Miner Hat'}
        ],
        bondedGenes: [
            {name: 'Klever', description: 'Ninja'},
            {name: 'Froday', description: 'Jason'},
            {name: 'Glub', description: 'Turkey Head'},
            {name: 'ARM', description: 'Sergio'},
        ]
      }
  },
  methods: {
    setPerfectAffinities: function () {
        if (this.devikinData.VitAffinity == 10 && this.perfectAffinities != null) {
            this.perfectAffinities += ', Vitality'
        } else if (this.devikinData.VitAffinity == 10 && this.perfectAffinities == null) {
            this.perfectAffinities = 'Vitality'
        }

        if (this.devikinData.PowAffinity == 10 && this.perfectAffinities != null) {
            this.perfectAffinities += ', Power'
        } else if (this.devikinData.PowAffinity == 10 && this.perfectAffinities == null) {
            this.perfectAffinities = 'Power'
        }

        if (this.devikinData.ForAffinity == 10 && this.perfectAffinities != null) {
            this.perfectAffinities += ', Fortitude'
        } else if (this.devikinData.ForAffinity == 10 && this.perfectAffinities == null) {
            this.perfectAffinities = 'Fortitude'
        }

        if (this.devikinData.AgiAffinity == 10 && this.perfectAffinities != null) {
            this.perfectAffinities += ', Agility'
        } else if (this.devikinData.AgiAffinity == 10 && this.perfectAffinities == null) {
            this.perfectAffinities = 'Agility'
        }

        if (this.devikinData.SanAffinity == 10 && this.perfectAffinities != null) {
            this.perfectAffinities += ', Sanity'
        } else if (this.devikinData.SanAffinity == 10 && this.perfectAffinities == null) {
            this.perfectAffinities = 'Sanity'
        }

        if (this.perfectAffinities == null) {
            this.perfectAffinities = 'None'
        }
    },
    setDevikinBondedStatus: function () {
        let bonded = this.devikinData.Set
        
        if (bonded == undefined) {
            this.bonded = 'No'
        } else if (bonded instanceof Object) {
            for (let index = 0; index < this.bondedGenes.length; index++) {
                if (this.bondedGenes[index].name == bonded.Name) {
                    this.bonded = this.bondedGenes[index].description
                    break
                }
            }
        }
    },
    setDevikinLimitedHat: function () {
        if (this.devikinData.Set) {
            this.hasLimitedHat = 'No'
        } else {
            for (const hat of this.limitedHats) {
                if (hat.name == this.devikinData.Hair.Name) {
                    this.hasLimitedHat = hat.description
                    break
                } else {
                    this.hasLimitedHat = 'No'
                }
            }
        }
    },
    setDevikinHardmintStatus: function () {
        this.devikinData.IsHardMinted? 
            this.isHardminted = 'Yes' : 
            this.isHardminted = 'No'
    },
    resetSearch: function () {
        this.perfectAffinities = null
    }
  }
}
</script>

<style scoped>

</style>
