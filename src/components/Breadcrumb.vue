<template>
  <div class="breadcrumb-section">
    <div class="container">
      <div class="row">
        <div class="col-lg-12">
          <div class="breadcrumb-text product-more">
            <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
            <span>{{ pageName }}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Breadcrumb",
  props: {
    pageName: String,
  },
};
</script>
