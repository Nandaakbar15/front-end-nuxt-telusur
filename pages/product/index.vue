<template>
  <div class="card">
    <div class="card-body">
      <Navbar />
      <h1>Daftar product</h1>
      <h3>
        <NuxtLink to="/product/create" class="btn btn-info"
          >Tambah Product</NuxtLink
        >
      </h3>
      <table class="table table-striped-columns">
        <thead>
          <tr>
            <th>ID Product</th>
            <th>Type</th>
            <th>Status</th>
            <th>Slug</th>
            <th>Title</th>
            <th>Description</th>
            <th>Media</th>
            <th>Price</th>
            <th>Sale Price</th>
            <th>Quantity</th>
            <th>SKU</th>
            <th>Weight</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(produk, index) in products" :key="index">
            <td>{{ produk.id }}</td>
            <td>{{ produk.type }}</td>
            <td>{{ produk.status }}</td>
            <td>{{ produk.slug }}</td>
            <td>{{ produk.title }}</td>
            <td>{{ produk.description }}</td>
            <td>{{ produk.media }}</td>
            <td>{{ produk.price }}</td>
            <td>{{ produk.salePrice }}</td>
            <td>{{ produk.quantity }}</td>
            <td>{{ produk.sku }}</td>
            <td>{{ produk.weight }}</td>
            <td>
              <NuxtLink :to="`/product/${produk.id}`" class="btn btn-success"
                >Edit</NuxtLink
              >
              <button
                class="btn btn-danger"
                type="button"
                @click="deleteProduct(produk.id)"
              >
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
      <NuxtLink to="/" class="btn btn-primary">Kembali</NuxtLink>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "product",
  data() {
    return {
      products: [],
    };
  },
  mounted() {
    this.getAllProduct();
  },
  methods: {
    getAllProduct() {
      axios
        .get("http://localhost:3000/api/shops/products")
        .then((response) => {
          console.log(response.data);
          this.products = response.data.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    deleteProduct(id) {
      if (confirm("Yakin mau hapus ini?")) {
        axios
          .delete(`http://localhost:3000/api/shops/products/${id}`)
          .then((response) => {
            console.log(response.data);
            this.getAllProduct();
          })
          .catch((error) => {
            console.log(error);
          });
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
