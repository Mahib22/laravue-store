<template>
  <div class="product">
    <Header />
    <Breadcrumb page-name="Detail" />
    <ProductDetail />
    <ProductRelated />
    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import Breadcrumb from "@/components/Breadcrumb.vue";
import ProductDetail from "@/components/ProductDetail.vue";
import ProductRelated from "../components/ProductRelated.vue";

export default {
  name: "ProductView",
  components: {
    Header,
    Footer,
    Breadcrumb,
    ProductDetail,
    ProductRelated,
  },
};
</script>
