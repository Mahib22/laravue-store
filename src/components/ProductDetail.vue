<template>
  <section class="product-shop spad page-details">
    <div class="container">
      <div class="row">
        <div class="col-lg-12">
          <div class="row">
            <div class="col-lg-6">
              <div class="product-pic-zoom">
                <img class="product-big-img" :src="image_default" alt="" />
              </div>
              <div class="product-thumbs">
                <Carousel
                  :items-to-show="3"
                  :wrap-around="true"
                  :autoplay="2000"
                >
                  <Slide
                    v-for="thumb in productDetails.galleries"
                    :key="thumb.id"
                    class="p-2"
                  >
                    <div
                      class="carousel__item pt"
                      :class="thumb.photo == image_default ? 'active' : ''"
                      @click="changeImage(thumb.photo)"
                    >
                      <img :src="thumb.photo" v-bind:alt="thumb.id" />
                    </div>
                  </Slide>
                </Carousel>
              </div>
            </div>
            <div class="col-lg-6">
              <div class="product-details">
                <div class="pd-title">
                  <span>{{ productDetails.type }}</span>
                  <h3>{{ productDetails.name }}</h3>
                </div>
                <div class="pd-desc">
                  <p v-html="productDetails.description"></p>
                  <h4>${{ productDetails.price }}</h4>
                </div>
                <div class="quantity">
                  <button
                    class="primary-btn pd-cart"
                    @click="saveCart(productDetails)"
                  >
                    Add To Cart
                  </button>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { Carousel, Slide } from "vue3-carousel";
import "vue3-carousel/dist/carousel.css";
import axios from "axios";

export default {
  name: "ProductDetail",

  components: {
    Carousel,
    Slide,
  },

  data() {
    return {
      image_default: "",
      productDetails: [],
      userCart: [],
    };
  },

  methods: {
    changeImage(urlImage) {
      this.image_default = urlImage;
    },

    setDataPicture(data) {
      this.productDetails = data;
      this.image_default = data.galleries[0].photo;
    },

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
      .get("http://shayna-backend.belajarkoding.com/api/products", {
        params: {
          id: this.$route.params.id,
        },
      })
      .then((res) => this.setDataPicture(res.data.data))
      .catch((err) => console.log(err));
  },
};
</script>
