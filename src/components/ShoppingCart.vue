<template>
  <section class="shopping-cart spad">
    <div class="container">
      <div class="row">
        <div class="col-lg-8">
          <div class="row">
            <div class="col-lg-12">
              <div class="cart-table">
                <table>
                  <thead>
                    <tr>
                      <th>Image</th>
                      <th class="p-name text-center">Product Name</th>
                      <th>Price</th>
                      <th>Action</th>
                    </tr>
                  </thead>
                  <tbody>
                    <tr v-for="cart in userCart" :key="cart.id">
                      <td class="cart-pic first-row">
                        <img class="photo-item" :src="cart.photo" />
                      </td>
                      <td class="cart-title first-row text-center">
                        <h5>{{ cart.name }}</h5>
                      </td>
                      <td class="p-price first-row">${{ cart.price }}</td>
                      <td class="delete-item" @click="removeItem(cart.index)">
                        <i class="material-icons"> close </i>
                      </td>
                    </tr>
                  </tbody>
                </table>
              </div>
            </div>
            <div class="col-lg-8">
              <h4 class="mb-4">Informasi Pembeli:</h4>
              <div class="user-checkout">
                <form>
                  <div class="form-group">
                    <label for="namaLengkap">Nama lengkap</label>
                    <input
                      type="text"
                      class="form-control"
                      id="namaLengkap"
                      aria-describedby="namaHelp"
                      placeholder="Masukan Nama"
                      v-model="customerInfo.name"
                    />
                  </div>
                  <div class="form-group">
                    <label for="namaLengkap">Email Address</label>
                    <input
                      type="email"
                      class="form-control"
                      id="emailAddress"
                      aria-describedby="emailHelp"
                      placeholder="Masukan Email"
                      v-model="customerInfo.email"
                    />
                  </div>
                  <div class="form-group">
                    <label for="namaLengkap">No. HP</label>
                    <input
                      type="text"
                      class="form-control"
                      id="noHP"
                      aria-describedby="noHPHelp"
                      placeholder="Masukan No. HP"
                      v-model="customerInfo.number"
                    />
                  </div>
                  <div class="form-group">
                    <label for="alamatLengkap">Alamat Lengkap</label>
                    <textarea
                      class="form-control"
                      id="alamatLengkap"
                      rows="3"
                      v-model="customerInfo.address"
                    ></textarea>
                  </div>
                </form>
              </div>
            </div>
          </div>
        </div>
        <div class="col-lg-4">
          <div class="row">
            <div class="col-lg-12">
              <div class="proceed-checkout">
                <ul>
                  <li class="subtotal">ID Transaction <span>#SH12000</span></li>
                  <li class="subtotal mt-3">
                    Subtotal <span>${{ totalPrice }}.00</span>
                  </li>
                  <li class="subtotal mt-3">Pajak <span>10%</span></li>
                  <li class="subtotal mt-3">
                    Total Biaya <span>${{ totalCost }}</span>
                  </li>
                  <li class="subtotal mt-3">
                    Bank Transfer <span>Mandiri</span>
                  </li>
                  <li class="subtotal mt-3">
                    No. Rekening <span>2208 1996 1403</span>
                  </li>
                  <li class="subtotal mt-3">Nama Penerima <span>Asep</span></li>
                </ul>
                <a @click="checkout()" class="proceed-btn"> I ALREADY PAID </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import axios from "axios";

export default {
  name: "ShoppingCart",

  data() {
    return {
      userCart: [],
      customerInfo: {
        name: "",
        email: "",
        number: "",
        address: "",
      },
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

    checkout() {
      let productIds = this.userCart.map(function (product) {
        return product.id;
      });

      let checkoutData = {
        name: this.customerInfo.name,
        email: this.customerInfo.email,
        number: this.customerInfo.number,
        address: this.customerInfo.address,
        transaction_total: this.totalCost,
        transaction_status: "PENDING",
        transaction_details: productIds,
      };

      axios
        .post(
          "http://shayna-backend.belajarkoding.com/api/checkout",
          checkoutData
        )
        .then(() => this.$router.push("success"))
        .catch((err) => console.log(err));
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

    totalCost() {
      let tax = (this.totalPrice * 10) / 100;
      return parseInt(this.totalPrice + tax);
    },
  },
};
</script>

<style scoped>
.photo-item {
  width: 100px;
  height: 100px;
}
</style>
