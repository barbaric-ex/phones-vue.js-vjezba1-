<template>
  <div class="col-4 nekimargin">
    <form action="" @submit.prevent="submitForm">
      <input
        type="number"
        v-model="id"
        placeholder="id"
        class="form-control"
      /><br />
      <input
        type="text"
        v-model="brand"
        placeholder="brand"
        class="form-control"
      /><br />
      <input
        type="text"
        v-model="name"
        placeholder="name"
        class="form-control"
      /><br />
      <input
        type="number"
        v-model="price"
        placeholder="price"
        class="form-control"
      /><br />

      <button type="submit" class="btn btn-primary form-control">
        Add Phone
      </button>
    </form>
  </div>
</template>

<script>
export default {
  emits: ["new-phone"],
  data() {
    return {
      id: null,
      brand: "",
      name: "",
      price: null,
    };
  },
  methods: {
    submitForm() {
      let newPhone = {
        id: this.id,
        brand: this.brand,
        name: this.name,
        price: this.price,
        available: true,
      };
      (this.id = null),
        (this.brand = ""),
        (this.name = ""),
        (this.price = null),
        this.$emit("new-phone", newPhone);
    },
  },
};
</script>

<style>
.nekimargin {
  margin-top: 100px;
  margin-bottom: 40px;
}
</style>
