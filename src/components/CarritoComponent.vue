<template>
  <div>
    <b-button @click="toggleCart" variant="outline-primary" class="floating-cart-btn custom-button">
  <b-icon icon="cart-fill"></b-icon>
</b-button>
<transition name="slide">


    <b-sidebar v-model="showCart" id="sidebar-cart" title="Carrito de Compras" right shadow class="custom-cart">
      <div v-if="quantity === 0" class="px-3 py-2">
        <p class="empty-cart-text">Agrega un producto para continuar</p>
      </div>
      <div v-else>
        <b-card
          v-for="(item, i) in items"
          :key="i"
          no-body
          class="overflow-hidden mb-3 custom-card"
          style="max-width: 540px"
        >
          <b-row no-gutters>
            <b-col md="6">
              <b-card-img :src="item.img" class="rounded-0"></b-card-img>
            </b-col>
            <b-col md="6">
              <b-card-body :title="item.name" class="card-body">
                <b-card-text>
                  <b-button-group class="float-center">
                    <b-button v-on:click="subtract(item)" variant="outline-primary">-</b-button>
                    <b-button disabled>{{ item.q }}</b-button>
                    <b-button v-on:click="add(item)" variant="outline-primary">+</b-button>
                  </b-button-group>
                </b-card-text>
              </b-card-body>
            </b-col>
          </b-row>
        </b-card>
      </div>

      <template #footer>
        <div class="d-flex bg-dark text-light align-items-center px-3 py-2">
          <strong class="mr-auto">Monto Total:</strong>
          <span class="total-price">{{ totalPrice | toPrice }}</span>

          <b-button @click="buy" id="buy-btn" variant="success">Pagar</b-button>
          <b-button @click="clearCart" variant="danger">Vaciar Carrito</b-button>
        </div>
      </template>
    </b-sidebar>
    </transition>
  </div>
</template>

<script>
import FiltersComponent from "./FiltersComponent.vue";

export default {
  name: "CarritoComponent",
  components: {},
  props: {
    items: {
      Array,
      required: true,
    },
  },
  mixins: [FiltersComponent],
  data() {
    return {
      showCart: false,
    };
  },
  computed: {
    quantity() {
      return this.$props.items.length;
    },
    totalPrice() {
      let price = 0;

      this.$props.items.forEach((item) => {
        price += item.price * item.q;
      });

      return price;
    },
  },
  methods: {
    toggleCart() {
      this.showCart = !this.showCart;
    },
    add(item) {
      item.q++;
    },
    subtract(item) {
      item.q === 0 ? (item.q = 0) : item.q--;
    },
    buy() {
      console.log("Iniciar compra...");
    },
    clearCart() {
      this.$emit('clear-cart');
    },
  },
};
</script>

<style scoped>
.custom-cart {
  background-color: #f8f8f8;
}

.d-flex.bg-dark.text-light.align-items-center {
  background-color: #343a40;
  color: #fff;
}

.empty-cart-text {
  font-family: Arial, sans-serif;
  font-size: 16px;
  color: #818181;
  text-align: center;
}

.custom-card {
  border: 1px solid #d8d8d8;
  border-radius: 4px;
  transition: box-shadow 0.3s ease-in-out;
}

.custom-card:hover {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.card-body {
  padding: 8px;
}

.floating-cart-btn {
  position: fixed;
  bottom: 20px;
  right: 20px;
  z-index: 999;
  font-size: 24px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #007bff;
  color: #fff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s ease-in-out;
}

.floating-cart-btn:hover {
  background-color: #0056b3;
}

.total-price {
  font-size: 18px;
  font-weight: bold;
  margin-right: 10px;
}

#buy-btn {
  margin-left: 2rem;
  font-size: 14px;
}

.custom-button {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: background-color 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
}

.custom-button:hover {
  background-color: #0056b3;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
}
</style>



