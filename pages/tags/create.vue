<template>
  <div class="card">
    <div class="card-body">
      <Navbar />
      <h1>Tambah Product Tag</h1>
      <form @submit.prevent="tambahTag()">
        <div class="mb-3">
          <input type="text" class="form-control" v-model="productTag.title" />
          <label class="form-check" for="title">Title</label>
        </div>
        <button type="submit" class="btn btn-primary">Tambah!</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "createProductTag",
  data() {
    return {
      productTag: {
        title: "",
      },
    };
  },
  methods: {
    tambahTag() {
      axios
        .post("http://localhost:3000/api/shops/tags", this.productTag)
        .then((response) => {
          console.log(response.data);
          alert("Tag berhasil ditambahkan");
          this.$router.push("/");
          this.resertForm();
        });
    },
    resertForm() {
      this.productTag.title = "";
    },
  },
};
</script>

<style lang="scss" scoped></style>
