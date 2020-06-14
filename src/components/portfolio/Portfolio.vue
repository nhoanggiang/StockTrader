<template>
  <div div class="row  mt-2">
    <app-stock v-for="stock in stocks" :stock="stock"></app-stock>
  </div>
</template>

<script>
import Stock from './Stock.vue'
import { mapGetters } from "vuex";

export default {
  computed: {
    ...mapGetters({
      stocks: "stockPortfolio"
    })
  },

  components: {
    appStock: Stock
  }
}
</script>

<style>

</style>
