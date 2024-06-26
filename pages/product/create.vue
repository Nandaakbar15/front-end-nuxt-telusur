<template>
  <div class="card">
    <div class="card-bod">
      <Navbar />
      <h1>Tambah Product</h1>
      <form @submit.prevent="tambahProduct()">
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
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "createProduct",
  data() {
    return {
      product: {
        type: "",
        status: "",
        slug: "",
        title: "",
        description: "",
        media: "",
        price: "",
        salePrice: "",
        quantity: "",
        sku: "",
        weight: "",
      },
    };
  },
  methods: {
    tambahProduct() {
      axios
        .post("http://localhost:3000/api/shops/products", this.product)
        .then((response) => {
          console.log(response.data);
          alert("Produk berhasil ditambahkan!");
          this.$router.push("/");
          this.resetForm();
        })
        .catch((error) => {
          console.log(error);
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
