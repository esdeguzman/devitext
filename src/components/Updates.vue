<template>
    <div :class="show">
        <div class="modal-background"></div>
        <div class="modal-card">
            <header class="modal-card-head">
            <p class="modal-card-title">Latest Updates</p>
            <button class="delete" aria-label="close" @click="closeModal"></button>
            </header>
            <section class="modal-card-body">
                <div v-for="update in updates" :key="update.id">
                    <p class="has-text-weight-bold mb-2">Date: {{ update.date }}</p>
                    <ul>
                        <li v-for="entry in update.entries" :key="entry.id" class="mb-1">
                            <span class="title is-size-6">{{ entry.name }}</span><br>
                            <span class="subtitle is-size-6">{{ entry.description }}</span>
                        </li>
                    </ul>
                    <hr>
                </div>
                <div class="columns">
                    <div class="column">
                        <h4>
                        <strong>Donate</strong>
                        </h4>
                        <a href="https://buymeacoffee.com/evilslime" target="_blank" class="button is-primary" style="margin-top: 10px;">
                            <span class="icon">
                                <img src="https://media.giphy.com/media/TDQOtnWgsBx99cNoyH/giphy.gif" alt="" height="50" width="50">
                            </span>
                            <span>Buy me a coffee</span>
                        </a>
                    </div>
                    <div class="column is-two-thirds">
                        <p>Your donation will be used for the site's maintenance like its monthly hosting, domain fees, etc.</p>
                    </div>
                </div>
            </section>
            <footer class="modal-card-foot">
            <button class="button is-link" @click="closeModal">Cool!</button>
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
                date: 'December 03, 2021',
                entries: [
                    {
                        name: 'Devitext Version 2.0',
                        description: 'Code has been migrated to VueJS components! Site\'s performance should slightly be boosted and more manageable source code for me :).'
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
