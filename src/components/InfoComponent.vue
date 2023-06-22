<template>
  <div>
    <b-modal id="modal-info" centered :title="item.name">
      <template #modal-header>
        <div class="text-center">
          <b-img rounded="top" :src="item.img" fluid></b-img>
        </div>
      </template>

      <h3 class="text-center">{{ item.name }}</h3>
      <p class="my-4 text-center">{{ item.price | toPrice }}</p>
      <p class="text-center">{{ item.desc }}</p>

      <template #modal-footer>
        <div class="d-flex justify-content-center align-items-center">
          <b-button-group>
            <b-button v-on:click="subtract" :disabled="quantity == 1">-</b-button>
            <b-button disabled>{{ quantity }}</b-button>
            <b-button v-on:click="add" :disabled="quantity >= item.stock">+</b-button>
          </b-button-group>

          <b-button v-on:click="addToCart()" variant="primary" class="ml-4">
            <b-icon icon="cart-plus" class="nav-icon mr-1"></b-icon>
            Agregar al carrito
          </b-button>
        </div>
      </template>
    </b-modal>
  </div>
</template>

<script>
import FiltersComponent from "./FiltersComponent.vue";

export default {
  name: "InfoComponent",
  props: {
    item: {
      type: Object,
      required: true,
    },
  },
  mixins: [FiltersComponent],
  data() {
    return {
      quantity: 1,
    };
  },
  methods: {
    addToCart() {
      console.log(`add to cart desde info: ${this.item.name}, q: ${this.quantity}`);

      let cartItem = {
        name: this.item.name,
        img: this.item.img,
        price: this.item.price,
        q: this.quantity,
      };

      this.$emit("addToCart", cartItem);
      this.$bvModal.hide("modal-info");

      this.quantity = 1;
    },
    add() {
      this.quantity++;
    },
    subtract() {
      this.quantity == 0 ? (this.quantity = 0) : this.quantity--;
    },
  },
};
</script>

<style scoped>
img {
  width: 100%;
  max-height: 20rem;
}

.modal-header {
  padding: 0;
}

.modal-footer {
  justify-content: center;
}

.text-center {
  text-align: center;
}

.ml-4 {
  margin-left: 1rem;
}

.nav-icon {
  margin-right: 0.5rem;
}



</style>
