<template>
  <tr>
    <td>{{ phone.id }}</td>
    <td @click="showBrand">{{ phone.brand }}</td>
    <td>{{ phone.name }}</td>
    <td>{{ phone.price }}</td>
    <td v-if="phone.available">
      <i @click="makePhoneUnavalible" class="bi bi-bag-check text-success"></i>
    </td>
    <td v-else>
      <i class="bi bi-bag-x text-danger"></i>
    </td>
    <td>
      <i
        @click="$emit('delete-phone', phone.id)"
        class="bi bi-trash-fill text-danger"
      ></i>
    </td>

    <td>
      <i class="bi bi-info-circle"></i>
    </td>
    <td>
      <i class="bi bi-shop"></i>
    </td>
  </tr>
</template>

<script>
export default {
  methods: {
    makePhoneUnavalible() {
      this.$emit("my-event", this.phone.id);
    },
    showBrand() {
      this.$emit("my-brand", this.phone.brand);
    },
  },

  mounted() {
    console.log("phone mounted");
  },

  updated() {
    console.log("phone updated");
  },

  unmounted() {
    console.log("phone deleted");
  },

  emits: ["my-event", "delete-phone"],
  props: {
    phone: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style></style>
