<template>
  <div class="card">
    <div class="card-body">
      <Navbar />
      <h1>Tambah Product Tag</h1>
      <form @submit.prevent="tambahCategories()">
        <div class="mb-3">
          <label class="form-check" for="title">Title</label>
          <input
            type="text"
            class="form-control"
            v-model="productCategory.title"
          />
        </div>
        <div class="mb-3">
          <label class="form-check" for="description">Description</label>
          <input
            type="text"
            class="form-control"
            v-model="productCategory.description"
          />
        </div>
        <button type="submit" class="btn btn-primary">Tambah!</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "createProductCategories",
  data() {
    return {
      productCategory: {
        title: "",
        description: "",
      },
    };
  },
  methods: {
    tambahCategories() {
      axios
        .post(
          "http://localhost:3000/api/shops/categories",
          this.productCategory
        )
        .then((response) => {
          console.log(response.data);
          alert("Produk Kategori berhasil ditambahkan");
          this.$router.push("/");
          this.resertForm();
        })
        .catch((error) => {
          console.log(error);
        });
    },
    resertForm() {
      this.productCategory.title = "";
      this.productCategory.description = "";
    },
  },
};
</script>

<style lang="scss" scoped></style>
