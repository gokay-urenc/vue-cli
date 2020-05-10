<template>
  <div class="text-center" id="list">
    <p v-if="products.length == 0">Product list is empty.</p>
    <table class="table table-dark" v-else>
      <thead>
        <tr>
          <th>ID</th>
          <th>Product Name</th>
          <th>Category ID</th>
          <th>Description</th>
          <th>Unit Price</th>
          <th>Stock</th>
          <th>Operations</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="product in products" :key="product.id">

          <td v-if="updateId === product.id">
            <input v-model="product.id" type="text" class="form-control" id="id" />
          </td>
          <td v-else>
            {{ product.id }}
          </td>

          <td v-if="updateId === product.id">
            <input v-model="product.productName" type="text" class="form-control" id="productName" />
          </td>
          <td v-else>
            {{ product.productName }}
          </td>

          <td v-if="updateId === product.id">
            <input v-model="product.categoryId" type="text" class="form-control" id="categoryId" />
          </td>
          <td v-else>
            {{ product.categoryId }}
          </td>

          <td v-if="updateId === product.id">
            <input v-model="product.quantityPerUnit" type="text" class="form-control" id="quantityPerUnit" />
          </td>
          <td v-else>
            {{ product.quantityPerUnit }}
          </td>

          <td v-if="updateId === product.id">
            <input v-model="product.unitPrice" type="text" class="form-control" id="unitPrice" />
          </td>
          <td v-else>
            {{ product.unitPrice }}
          </td>

          <td v-if="updateId === product.id">
            <input v-model="product.unitsInStock" type="text" class="form-control" id="unitsInStock" />
          </td>
          <td v-else>
            {{ product.unitsInStock }}
          </td>

          <td v-if="updateId !== product.id">
            <button class="btn btn-primary mr-2" @click="handleUpdate(product)">
              Update
            </button>
            <button class="btn btn-danger" @click="handleDelete(product)">
              Delete
            </button>
          </td>

          <td v-else>
            <button class="btn btn-success mr-2" @click="handleSave(product)">
              Save
            </button>
            <button class="btn btn-secondary" @click="handleCancel">
              Cancel
            </button>
          </td>

        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "product-list",
  data() {
    return {
      updateId: null
    };
  },
  props: {
    products: Array
  },
  methods: {
    handleDelete(product) {
      this.$emit("delete:product", product);
    },
    handleUpdate(product) {
      this.updateId = product.id;
    },
    handleSave(product) {
      this.$emit("update:product", product);
      this.updateId = null;
    },
    handleCancel() {
      this.updateId = null;
    }
  }
};
</script>

<style scoped>
#list {
  margin: 100px;
}
</style>