<template>
  <section class="history">
    <h2 class="section-title">Favorite Phrases</h2>
    <ul class="history-list">
      <li v-for="(item, index) of favPhrases" :key="index + item">
        <button class="btn" @click="restore(index)">restore</button>
        <button class="btn" @click="remove(index)">remove</button>
        <span class="history-list__branch-name" @click="copy">{{ item }}</span>
      </li>
    </ul>
  </section>
</template>

<script>
import { mapState } from 'vuex';
import { copyText } from '../scripts/helper';

export default {
  computed: mapState(['favPhrases']),
  methods: {
    restore(index) {
      this.$store.commit('formData/set', ['summary', this.favPhrases[index]]);
      document.getElementsByClassName('commit-summery')[0].focus();
    },
    remove(index) {
      this.$store.dispatch('favPhrases/remove', index);
    },
    copy($event) {
      copyText($event.target.textContent);
    },
  },
};
</script>
