<template>
  <div class="card">
    <div class="card-body">
      <Navbar />
      <h1>Ubah Product Tag</h1>
      <form @submit.prevent="ubahCategories()">
        <div class="mb-3">
          <label class="form-check" for="title">Title</label>
          <input
            type="text"
            class="form-control"
            v-model="productCategory.title"
          />
        </div>
        <div class="mb-3">
          <label class="form-check" for="title">Description</label>
          <input
            type="text"
            class="form-control"
            v-model="productCategory.description"
          />
        </div>
        <button type="submit" class="btn btn-primary">ubah!</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "updateProductCategories",
  data() {
    return {
      id: "",
      productCategory: {},
    };
  },
  mounted() {
    this.id = this.$route.params.id;
    this.getCategories(this.id);
  },
  methods: {
    getCategories(id) {
      axios
        .get(`http://localhost:3000/api/shops/categories/${id}`)
        .then((response) => {
          console.log(response.data);
          this.productCategory = response.data.data;
        });
    },
    ubahCategories() {
      axios
        .patch(
          `http://localhost:3000/api/shops/categories/${this.id}`,
          this.productCategory
        )
        .then((response) => {
          console.log(response.data);
          alert("Produk Kategori berhasil di ubah!");
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
