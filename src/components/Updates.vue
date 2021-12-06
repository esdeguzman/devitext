<template>
    <div :class="show">
        <div class="modal-background"></div>
        <div class="modal-card">
            <header class="modal-card-head">
            <p class="modal-card-title">Latest Updates</p>
            <button class="delete" aria-label="close" @click="closeModal"></button>
            </header>
            <section class="modal-card-body">
            <!-- Content ... -->
            </section>
            <footer class="modal-card-foot">
            <button class="button is-link is-pulled-right" @click="closeModal">Cool!</button>
            </footer>
        </div>
    </div>
</template>

<script>
import Vue from '../../node_modules/vue'

export default {
  name: 'Updates',
  props: {
      bus: Vue
  },
  mounted() {
      this.bus.$on('view-patches', () => {
          this.openModal()
      })
  },
  data() {
      return {
          update: true,
          showed: false,
          show: 'modal',
          updates: [
            {
                date: 'December 06, 2021',
                entries: [
                    {
                        name: 'Fixed Devikin ID Display',
                        description: 'Site is now properly displaying ID of Devikin with value of 0 properly.'
                    },
                    {
                        name: 'Viewing NFT to KleverNFT site',
                        description: 'Button is now provided so you can view youre Devikin in KleverNFT site.'
                    },
                    {
                        name: 'Patches Link',
                        description: 'Patches are now available for viewing!'
                    }
                ]
            },
            {
                name: 'Devitext Version 2.0',
                entries: [
                    {
                        date: 'December 03, 2021',
                        description: 'Code has been overhauled to VueJS components! Site\'s performance should slightly be boosted and more manageable source code for me :).'
                    }
                ]
            }
          ]
      }
  },
  methods: {
      closeModal: function () {
          this.show = 'modal'
      },
      openModal: function () {
          this.show = 'modal is-active'
      }
  }
}
</script>

<style scoped>

</style>
