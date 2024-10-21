<template>
  <div :class="{ 'col-12': !displayForm, 'col-8': displayForm }">
    <table class="table table-striped table-bordered table-hover table-dark">
      <thead>
        <tr>
          <th>ID</th>
          <th>Brand</th>
          <th>Name</th>
          <th>Price</th>
          <th>Avalible</th>
          <th>Delete</th>
          <th>Spec</th>
          <th>Store</th>
        </tr>
      </thead>
      <tbody>
        <mobile-phone
          @display-modal="displayModal"
          @delete-phone="deletePhone"
          @my-brand="showBrandName"
          @my-event="changeAvalible"
          v-for="phone in phones"
          :phone="phone"
          :key="phone.id"
        ></mobile-phone>
      </tbody>
    </table>
  </div>
  <custom-modal v-if="display">
    <template #default v-if="specs">
      <h1>Spec</h1>
      <p>{{ currentPhone.specification }}</p>
    </template>

    <template #stores v-if="stores">
      <h1>Stores</h1>
      <p v-for="store in currentPhone.stores">{{ store }}</p>
    </template>
  </custom-modal>
</template>

<script>
import CustomModal from "./CustomModal.vue";
import MobilePhone from "./MobilePhone.vue";
export default {
  data() {
    return {
      display: false,
      currentPhone: {},
      specs: false,
      stores: false,
    };
  },
  props: {
    phones: {
      type: Array,
      required: true,
    },
    displayForm: {
      type: Boolean,
      required: false,
    },
  },
  components: { MobilePhone, CustomModal },
  methods: {
    changeAvalible(id) {
      this.$emit("change-phone", id);
    },
    showBrandName(brand) {
      this.$emit("show-brand", brand);
    },
    deletePhone(id) {
      this.$emit("delete-phone", id);
    },

    displayModal(phone, mode) {
      this.display = !this.display;
      this.currentPhone = phone;
      this.stores = false;
      this.specs = false;
      this[mode] = true;
    },
  },
  emits: ["change-phone", "delete-phone"],
};
</script>

<style></style>
