<template>
  <div class="card">
    <div class="card-body">
      <Navbar />
      <h1>Daftar product category</h1>
      <table class="table table-striped-columns">
        <thead>
          <tr>
            <th>ID Product Category</th>
            <th>Title</th>
            <th>Description</th>
            <th>ParentId</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(p, index) in productCategory" :key="index">
            <td>{{ p.id }}</td>
            <td>{{ p.title }}</td>
            <td>{{ p.description }}</td>
            <td>{{ p.parentId }}</td>
            <td>
              <NuxtLink :to="`/productCategory/${p.id}`" class="btn btn-success"
                >Edit</NuxtLink
              >
              <button
                class="btn btn-danger"
                type="button"
                @click="deleteProduct(p.id)"
              >
                Delete
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "productCategory",
  data() {
    return {
      productCategory: [],
    };
  },
  mounted() {
    this.getAllProductCategory();
  },
  methods: {
    getAllProductCategory() {
      axios
        .get("http://localhost:3000/api/shops/categories")
        .then((response) => {
          console.log(response.data.data);
          this.productCategory = response.data.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    deleteProductCategory(id) {
      if (confirm("Yakin mau hapus ini?")) {
        axios
          .delete(`http://localhost:3000/api/shops/categories/${id}`)
          .then((response) => {
            console.log(response.data);
            alert("Product category berhasil dihapus!");
            this.getAllProductCategory();
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
