<template>
  <div class="col-sm-6 col-md-6 col-lg-6 mt-4">
    <div class="card">
      <div class="card-heading bg-success">
        <h4 class="card-title">
          {{ stock.name }}
          <small>(Price: {{ stock.price }} | Quantity: {{ stock.quantity }})</small>
        </h4>
      </div>
      <div class="card-body">
        <div class="float-left">
          <input
            type="number"
            min="0"
            class="form-control"
            placeholder="Quantity"
            v-model.number="quantity"
            :class="{danger: insufficientQuantity}"
          />
        </div>
        <div class="float-right">
          <button
            class="btn btn-success"
            @click="sellStock"
            :disabled="insufficientQuantity || quantity <= 0 || !Number.isInteger(quantity)"
          >
            {{ insufficientQuantity ? 'Not enough' : 'Sell' }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {mapActions} from 'vuex';
export default {
  props: ["stock"],

  data() {
    return {
      quantity: 0
    };
  },

  computed: {
    insufficientQuantity() {
      return this.quantity > this.stock.quantity;
    }
  },

  methods: {
    ...mapActions({
      placeSellOrder: 'sellStock'
  }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      };
      this.placeSellOrder(order);
      this.quantity = 0;
    }
  }
};
</script>

<style scoped>
  .danger {
    border: 1px solid red;
  }
</style>
