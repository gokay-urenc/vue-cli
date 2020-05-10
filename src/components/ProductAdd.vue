<template>
  <div id="form">
    <form class="font-weight-bold" @submit.prevent="handleAdd">

      <div class="form-group">
        <label for="productName">Product Name</label>
        <input v-model="product.productName" type="text" class="form-control" id="productName" />
      </div>

      <div class="form-group">
        <label for="categoryId">Category ID</label>
        <input v-model="product.categoryId" type="text" class="form-control" id="categoryId" />
      </div>

      <div class="form-group">
        <label for="quantityPerUnit">Description</label>
        <input v-model="product.quantityPerUnit" type="text" class="form-control" id="quantityPerUnit" />
      </div>

      <div class="form-group">
        <label for="unitPrice">Unit Price</label>
        <input v-model="product.unitPrice" type="text" class="form-control" id="unitPrice" />
      </div>

      <div class="form-group">
        <label for="unitsInStock">Stock</label>
        <input v-model="product.unitsInStock" type="text" class="form-control" id="unitsInStock" />
      </div>

      <button type="submit" class="btn btn-success">Add</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "product-add",
  data() {
    return {
      product: {
        id: "",
        productName: "",
        categoryId: "",
        quantityPerUnit: "",
        unitPrice: "",
        unitsInStock: ""
      }
    };
  },
  methods: {
      handleAdd() {
          this.$emit("add:product", this.product);
      }
  }
};
</script>

<style scoped>
#form {
  margin: 30px 100px 100px 100px;
}
</style>