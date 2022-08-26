<template>
  <div class="cart">
    <Header />
    <Breadcrumb page-name="Shopping Cart" />
    <ShoppingCart />
    <Footer />
  </div>
</template>

<script>
import Header from "../components/Header.vue";
import Breadcrumb from "../components/Breadcrumb.vue";
import Footer from "../components/Footer.vue";
import ShoppingCart from "../components/ShoppingCart.vue";

export default {
  name: "CartView",
  components: {
    Header,
    Breadcrumb,
    Footer,
    ShoppingCart,
  },
};
</script>
