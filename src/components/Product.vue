<template>
  <div class="container">
    <div class="row" v-if="products.length > 0">
      <div class="col-md-4" v-for="product in products" :key="product.id">
        <div class="product-item">
          <div class="pi-pic">
            <img
              v-bind:src="product.galleries[0].photo"
              v-bind:alt="product.name"
            />
            <ul>
              <li class="w-icon active">
                <a @click="saveCart(product)"><i class="icon_bag_alt"></i></a>
              </li>
              <li class="quick-view">
                <router-link v-bind:to="`/product/${product.id}`"
                  >+ Quick View</router-link
                >
              </li>
            </ul>
          </div>
          <div class="pi-text">
            <div class="catagory-name">{{ product.type }}</div>
            <a href="#">
              <h5>{{ product.name }}</h5>
            </a>
            <div class="product-price">${{ product.price }}</div>
          </div>
        </div>
      </div>
    </div>

    <div class="col-md-12" v-else>
      <h3 class="text-center">Produk tidak tersedia</h3>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Product",

  data() {
    return {
      products: [],
      userCart: [],
    };
  },

  methods: {
    saveCart(product) {
      let productStored = {
        id: product.id,
        name: product.name,
        price: product.price,
        photo: product.galleries[0].photo,
      };

      this.userCart.push(productStored);
      const parsed = JSON.stringify(this.userCart);
      localStorage.setItem("userCart", parsed);
    },
  },

  mounted() {
    if (localStorage.getItem("userCart")) {
      try {
        this.userCart = JSON.parse(localStorage.getItem("userCart"));
      } catch (e) {
        localStorage.removeItem("userCart");
      }
    }

    axios
      .get("http://shayna-backend.belajarkoding.com/api/products")
      .then((res) => (this.products = res.data.data.data))
      .catch((err) => console.log(err));
  },
};
</script>
