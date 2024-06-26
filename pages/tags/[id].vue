<template>
  <div class="card">
    <div class="card-body">
      <Navbar />
      <h1>Ubah Product Tag</h1>
      <form @submit.prevent="ubahTag()">
        <div class="mb-3">
          <label class="form-check" for="title">Title</label>
          <input type="text" class="form-control" v-model="productTag.title" />
        </div>
        <button type="submit" class="btn btn-primary">Ubah!</button>
      </form>
      <br />
      <NuxtLink to="/" class="btn btn-primary">Kembali</NuxtLink>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "updateTag",
  data() {
    return {
      id: "",
      productTag: {},
    };
  },
  mounted() {
    this.id = this.$route.params.id;
    this.getTag(this.id);
  },
  methods: {
    getTag(id) {
      axios
        .get(`http://localhost:3000/api/shops/tags/${id}`)
        .then((response) => {
          console.log(response.data);
          this.productTag = response.data.data;
        });
    },
    ubahTag() {
      axios
        .patch(`http://localhost:3000/api/shops/tags/${this.id}`, this.product)
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
      this.productTag.title = "";
    },
  },
};
</script>

<style lang="scss" scoped></style>
