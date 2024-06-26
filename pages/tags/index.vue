<template>
  <div class="card">
    <div class="card-body">
      <Navbar />
      <h1>Product Tags</h1>
      <h3>
        <NuxtLink to="/tags/create" class="btn btn-info"
          >Tambah Product Tag</NuxtLink
        >
      </h3>
      <table class="table table-striped-columns">
        <thead>
          <tr>
            <th>ID Product Category</th>
            <th>Title</th>
            <th>Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(p, index) in productTag" :key="index">
            <td>{{ p.id }}</td>
            <td>{{ p.title }}</td>
            <td>
              <NuxtLink :to="`/tags/${p.id}`" class="btn btn-success"
                >Edit</NuxtLink
              >
              <button
                class="btn btn-danger"
                type="button"
                @click="deleteProductTag(p.id)"
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
  name: "productTags",
  data() {
    return {
      productTag: [],
    };
  },
  mounted() {
    this.getAllTags();
  },
  methods: {
    getAllTags() {
      axios
        .get("http://localhost:3000/api/shops/tags")
        .then((response) => {
          console.log(response.data.data);
          this.productTag = response.data.data;
        })
        .catch((error) => {
          console.log(error);
        });
    },
    deleteProductTag(id) {
      if (confirm("Yakin mau hapus ini?")) {
        axios
          .delete(`http://localhost:3000/api/shops/tags/${id}`)
          .then((response) => {
            console.log(response.data);
            this.getAllTags();
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
