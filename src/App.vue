<template>
  <div class="container">
    <div class="row">
      <h1>
        Phones App
        <button @click="toggleForm" class="btn btn-success btn-sm">
          {{ sign }}
        </button>
      </h1>

      <div class="col-12 search_div">
        <input
          type="text"
          v-model="searchTerm"
          placeholder="search"
          class="form-control"
        />
      </div>
      <add-phone v-if="displayForm" @new-phone="savePhone"></add-phone>
      <phones-table
        :displayForm="displayForm"
        @delete-phone="deletePhone"
        @show-brand="finalName"
        @change-phone="finalChange"
        :phones="filteredPhones"
      ></phones-table>
    </div>
  </div>
</template>

<script>
import AddPhone from "./components/AddPhone.vue";
import PhonesTable from "./components/PhonesTable.vue";
export default {
  data() {
    return {
      sign: "+",
      displayForm: false,
      phones: [],
      searchTerm: "",
    };
  },
  methods: {
    finalChange(id) {
      let currentPhone = this.phones.find((phone) => phone.id === id);
      currentPhone.available = false;
    },

    toggleForm() {
      this.displayForm = !this.displayForm;
      this.displayForm ? (this.sign = "-") : (this.sign = "+");
    },
    finalName(brand) {
      let currentBrand = (this.phones.brand = brand);
      alert(currentBrand);
    },
    savePhone(newPhone) {
      this.phones.push(newPhone);
    },
    deletePhone(id) {
      this.phones = this.phones.filter((phone) => phone.id !== id);
    },
  },

  computed: {
    filteredPhones() {
      if (this.searchTerm.length === 0) {
        return this.phones;
      } else {
        let filter = this.phones.filter((phone) =>
          phone.name.includes(this.searchTerm)
        );
        return filter;
      }
    },
  },

  mounted() {
    fetch(
      "https://raw.githubusercontent.com/Danilovesovic/pitanja/main/phones.json"
    )
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        this.phones = data;
      });
  },
  components: { PhonesTable, AddPhone },
};
</script>

<style>
.search_div {
  margin-bottom: 20px;
}
</style>
