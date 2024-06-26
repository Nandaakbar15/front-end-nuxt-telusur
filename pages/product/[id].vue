<template>
  <div class="card">
    <div class="card-body">
      <Navbar />
      <h1>Tambah Product</h1>
      <form @submit.prevent="ubahProduct()">
        <div class="mb-3">
          <label for="type" class="form-label">Type</label>
          <select name="type" v-model="product.type">
            <option value="SIMPLE">Single</option>
            <option value="VARIABLE">Variable</option>
          </select>
        </div>
        <div class="mb-3">
          <label for="status" class="form-label">Status</label>
          <select name="status" v-model="product.status">
            <option value="DRAFT">Draft</option>
            <option value="ACTIVE">Active</option>
          </select>
        </div>
        <div class="mb-3">
          <label class="form-check" for="slug">Slug</label>
          <input type="text" class="form-control" v-model="product.slug" />
        </div>
        <div class="mb-3">
          <label class="form-check" for="title">Title</label>
          <input type="text" class="form-control" v-model="product.title" />
        </div>
        <div class="mb-3">
          <label class="form-check" for="description">Description</label>
          <input
            type="text"
            class="form-control"
            v-model="product.description"
          />
        </div>
        <div class="mb-3">
          <label class="form-check" for="media">Media</label>
          <input type="text" class="form-control" v-model="product.media" />
        </div>
        <div class="mb-3">
          <label class="form-check" for="price">Price</label>
          <input type="text" class="form-control" v-model="product.price" />
        </div>
        <div class="mb-3">
          <label class="form-check" for="salePrice">Sale Price</label>
          <input type="text" class="form-control" v-model="product.salePrice" />
        </div>
        <div class="mb-3">
          <label class="form-check" for="sku">Sku</label>
          <input type="text" class="form-control" v-model="product.sku" />
        </div>
        <div class="mb-3">
          <label class="form-check" for="weight">Weight</label>
          <input type="text" class="form-control" v-model="product.weight" />
        </div>
        <div class="mb-3">
          <label class="form-check" for="weight">Quantity</label>
          <input type="text" class="form-control" v-model="product.quantity" />
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
      <br />
      <NuxtLink to="/" class="btn btn-primary">Kembali</NuxtLink>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "updateProduct",
  data() {
    return {
      id: "",
      product: {},
    };
  },
  mounted() {
    this.id = this.$route.params.id;
    this.getProduct(this.id);
  },
  methods: {
    getProduct(id) {
      axios
        .get(`http://localhost:3000/api/shops/products/${id}`)
        .then((response) => {
          console.log(response.data);
          this.product = response.data.data;
        });
    },
    ubahProduct() {
      axios
        .patch(
          `http://localhost:3000/api/shops/products/${this.id}`,
          this.product
        )
        .then((response) => {
          console.log(response.data);
          alert("Product berhasil diubah!");
          this.$router.push("/"); // kembali ke halaman home
          this.resetForm();
        })
        .catch((error) => {
          console.log(error);
          this.error =
            "Failed to change the product. " +
            (error.response?.data?.message || "");
        });
    },
    resetForm() {
      this.product.type = "";
      this.product.status = "";
      this.product.slug = "";
      this.product.title = "";
      this.product.description = "";
      this.product.media = "";
      this.product.price = "";
      this.product.salePrice = "";
      this.product.quantity = "";
      this.product.sku = "";
      this.product.weight = "";
    },
  },
};
</script>

<style lang="scss" scoped></style>
