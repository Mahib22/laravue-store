<template>
  <header class="header-section">
    <div class="container">
      <div class="inner-header">
        <div class="row">
          <div class="col-lg-2 col-md-2">
            <div class="logo">
              <router-link to="/" class="text-dark h5 text-uppercase"
                >laravue store</router-link
              >
            </div>
          </div>
          <div class="col-lg-7 col-md-7"></div>
          <div class="col-lg-3 text-right col-md-3">
            <ul class="nav-right">
              <li class="cart-icon">
                Keranjang Belanja &nbsp;
                <a href="#">
                  <i class="icon_bag_alt"></i>
                  <span>{{ userCart.length }}</span>
                </a>
                <div class="cart-hover">
                  <div class="select-items">
                    <table>
                      <tbody v-if="userCart.length > 0">
                        <tr v-for="cart in userCart" :key="cart.id">
                          <td class="si-pic">
                            <img class="photo-item" :src="cart.photo" alt="" />
                          </td>
                          <td class="si-text">
                            <div class="product-selected">
                              <p>${{ cart.price }} x 1</p>
                              <h6>{{ cart.name }}</h6>
                            </div>
                          </td>
                          <td @click="removeItem(cart.id)" class="si-close">
                            <i class="ti-close"></i>
                          </td>
                        </tr>
                      </tbody>
                      <tbody v-else>
                        <tr>
                          <td>Keranjang Kosong</td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                  <div class="select-total">
                    <span>total:</span>
                    <h5>${{ totalPrice }}.00</h5>
                  </div>
                  <div class="select-button">
                    <router-link to="/cart" class="primary-btn view-card"
                      >VIEW CARD</router-link
                    >
                    <a href="#" class="primary-btn checkout-btn">CHECK OUT</a>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",

  data() {
    return {
      userCart: [],
    };
  },

  methods: {
    removeItem(idx) {
      let cartUserStorage = JSON.parse(localStorage.getItem("userCart"));
      let itemCartUserStorage = cartUserStorage.map(
        (itemCartUserStorage) => itemCartUserStorage.id
      );
      let index = itemCartUserStorage.findIndex((id) => id == idx);

      this.userCart.splice(index, 1);
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
  },

  computed: {
    totalPrice() {
      return this.userCart.reduce(function (items, data) {
        return items + data.price;
      }, 0);
    },
  },
};
</script>

<style scoped>
.photo-item {
  width: 80px;
  height: 80px;
}
</style>
