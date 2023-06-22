<template>
  <div>
    <header id="cabecera" class="col-12">
      <h1 class="navbar-title">DENIS BIKE SHOP</h1>
    </header>


    <div class="navbar-wrapper">
      <b-navbar class="navbar navbar-expand-lg">
        <div class="container-fluid">
          <b-navbar-nav class="nav-item">
            <b-nav-item href="#" class="nav-link">Accesorios</b-nav-item>
            <b-nav-item href="#" class="nav-link">Service de Bicicleta</b-nav-item>
            <b-nav-item href="#" class="nav-link" @click="submitLogin">Contactenos</b-nav-item>
          </b-navbar-nav>

          <b-navbar-brand href="#" @click="backToHome" class="navbar-brand">
            <h2 class="navbar-title">Denis Bike-Shop</h2>
          </b-navbar-brand>
<!--Falta aplicar para buscar el elemento -->
          <b-navbar-nav class="search-bar">
          <input type="text" v-model="searchQuery" placeholder="Buscar...">
          <button @click="searchItems">Buscar</button>
          </b-navbar-nav>
          <ul>
            <li v-for="result in searchResults" :key="result.id">
                {{ result.name }}
                 </li>
          </ul>

          <b-navbar-nav class="ml-auto">
            <b-button class="nav-btn" @click="submitLogin">Usuario</b-button>
            <b-button v-b-toggle.sidebar-cart class="nav-btn">
              <b-icon icon="cart" class="nav-icon"></b-icon>
              <div v-if="cartQ > 0" class="cart-dot">
                <p class="cart-total">{{ cartQ }}</p>
              </div>
            </b-button>
          </b-navbar-nav>
        </div>
      </b-navbar>
    </div>
  </div>
</template>

<script>
export default {
  name: "NavbarComponent",
  components: {},
  props: {
    cartQ: Number,
    items: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      searchQuery: '',
      searchResults: []
    };
  },
  methods: {
    submitLogin() {
      this.$emit("login", true);
    },
    backToHome() {
      this.$emit("login", false);
    },
  //Falta aplicar para que busque el elemento//
searchItems() {
  if (this.searchQuery.trim() === '') {
    // Si la búsqueda está vacía, restablecer los resultados de búsqueda
    this.searchResults = [];
  } else {
    // Realizar la búsqueda
    const searchTerm = this.searchQuery.toLowerCase();
    this.searchResults = this.items.filter(item => {
      return item.name.toLowerCase().includes(searchTerm);
    });
  }
}
  }
};


</script>

<style scoped>
#cabecera {
  background-image: url("../assets/images/My\ project.jpg");
  background-size: cover;
  height: auto;
  z-index: 2;
}

#cabecera h1 {
  margin-bottom: 2px;
  text-align: left;
  padding-top: 60px;
  font: fantasy 30px oblique;
  color: #29a718;
}

.navbar-wrapper {
  position: relative;
  z-index: 1;
}

.navbar {
  width: 100%;
  min-width: 25rem;
  min-height: 5rem;
  z-index: 12;
  color: crimson;
  text-decoration: none;
  background: rgba(108, 189, 236, 0.3);
  backdrop-filter: blur(5px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.navbar-title {
  position: relative;
  font-family: "Arial Black", sans-serif;
  text-align: center;
  margin-bottom: 0;
}

.navbar-light .navbar-brand {
  color: crimson;
}

.nav-item {
  font-family: 'Times New Roman', Times, serif;
  font-size: 16px;
}

.nav-icon {
  color: crimson;
}

.nav-btn {
  align-content: space-around;
  font-family: Arial, sans-serif;
  font-weight: bold;
  font-size: 18px;
  padding: 12px 20px;
  border-radius: 30px;
  background-color: #e6f2e6;
  border: none;
  color: crimson;
  margin-left: 10px;
}

.nav-btn:hover {
  background-color: #c5e6c5;
}

.cart-dot {
  height: 2rem;
  width: 2rem;
  background-color: crimson;
  border-radius: 50%;
  z-index: 3;
  position: absolute;
  bottom: 1.8rem;
  right: 0.4rem;
}

.cart-total {
  color: #fff;
  font-size: 1rem;
  text-align: center;
  margin-top: 2px;
}

.search-bar {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.search-bar input {
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

.search-bar button {
  margin-left: 10px;
  padding: 8px 16px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  cursor: pointer;
}


</style>
