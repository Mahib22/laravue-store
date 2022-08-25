<template>
  <div class="home">
    <Header />
    <Product />
    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import Product from "@/components/Product.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "HomeView",
  components: {
    Header,
    Product,
    Footer,
  },
};
</script>
