<template>
  <div id="app">
    <!--
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Vue JS" :nmbr="5" />
    -->
    <ProductAdd @add:product="addProduct" />
    <ProductList :products="products" @delete:product="deleteProduct" @update:product="updateProduct" />
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import ProductList from "./components/ProductList.vue";
import ProductAdd from "./components/ProductAdd.vue";

export default {
  name: "app",

  components: {
    //HelloWorld,
    ProductList,
    ProductAdd
  },

  data() {
    return {
      products: []
    };
  },

  mounted() {
    this.getProducts();
  },

  methods: {
    async getProducts() {
      const result = await fetch("http://localhost:3000/products");
      const data = await result.json();
      this.products = data;
    },

    async deleteProduct(product) {
      await fetch('http://localhost:3000/products/' + product.id, {
        method: "DELETE"
      });
      this.products = this.products.filter(p => p.id !== product.id);
    },

    async updateProduct(product) {
      const result = await fetch('http://localhost:3000/products/' + product.id, {
        method: "PUT",
        body: JSON.stringify(product),
        headers: { "Content-Type" : "application/json" }
      });
      const updatedProduct = await result.json();
      this.products = this.products.map(p => p.id === product.id ? updatedProduct : product);
    },

    async addProduct(product) {
      const result = await fetch('http://localhost:3000/products', {
        method: "POST",
        body: JSON.stringify(product),
        headers: { "Content-Type" : "application/json" }
      });
      const addedProduct = await result.json();
      this.products = [...this.products, addedProduct];
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>