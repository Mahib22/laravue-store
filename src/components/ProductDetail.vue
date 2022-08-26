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
                  <Slide v-for="thumb in thumbs" :key="thumb" class="p-2">
                    <div
                      class="carousel__item pt"
                      :class="thumb == image_default ? 'active' : ''"
                      @click="changeImage(thumb)"
                    >
                      <img :src="thumb" alt="" />
                    </div>
                  </Slide>
                </Carousel>
              </div>
            </div>
            <div class="col-lg-6">
              <div class="product-details">
                <div class="pd-title">
                  <span>oranges</span>
                  <h3>Pure Pineapple</h3>
                </div>
                <div class="pd-desc">
                  <p>
                    Lorem ipsum dolor sit, amet consectetur adipisicing elit.
                    Quam possimus quisquam animi, commodi, nihil voluptate
                    nostrum neque architecto illo officiis doloremque et
                    corrupti cupiditate voluptatibus error illum. Commodi
                    expedita animi nulla aspernatur. Id asperiores blanditiis,
                    omnis repudiandae iste inventore cum, quam sint molestiae
                    accusamus voluptates ex tempora illum sit perspiciatis.
                    Nostrum dolor tenetur amet, illo natus magni veniam quia sit
                    nihil dolores. Commodi ratione distinctio harum voluptatum
                    velit facilis voluptas animi non laudantium, id dolorem
                    atque perferendis enim ducimus? A exercitationem recusandae
                    aliquam quod. Itaque inventore obcaecati, unde quam impedit
                    praesentium veritatis quis beatae ea atque perferendis
                    voluptates velit architecto?
                  </p>
                  <h4>$495.00</h4>
                </div>
                <div class="quantity">
                  <a href="shopping-cart.html" class="primary-btn pd-cart"
                    >Add To Cart</a
                  >
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

export default {
  name: "ProductDetail",
  components: {
    Carousel,
    Slide,
  },
  data() {
    return {
      image_default: "img/mickey1.jpg",
      thumbs: [
        "img/mickey1.jpg",
        "img/mickey2.jpg",
        "img/mickey3.jpg",
        "img/mickey4.jpg",
      ],
    };
  },
  methods: {
    changeImage(urlImage) {
      this.image_default = urlImage;
    },
  },
};
</script>
