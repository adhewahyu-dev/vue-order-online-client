<template>
  <div class="searchform">
    <h4>Find Username</h4>
    <div class="form-group">
      <input type="text" class="form-control" id="username" required v-model="username" name="username">
    </div>
 
    <div class="btn-group">
      <button v-on:click="searchCustomers" class="btn btn-success">Search</button>
    </div>
 
    <ul class="search-result">
      <li v-for="(customer, index) in customers" :key="index">
        <h6>{{customer.fullname}} ({{customer.username}})</h6>
      </li>
    </ul>
  </div>
</template>
 
<script>
import http from "../http-common";
 
export default {
  name: "search-customer",
  data() {
    return {
      age: 0,
      customers: []
    };
  },
  methods: {
    /* eslint-disable no-console */
    searchCustomers() {
      http
        .get("/customers/age/" + this.age)
        .then(response => {
          this.customers = response.data; // JSON are parsed automatically.
          console.log(response.data);
        })
        .catch(e => {
          console.log(e);
        });
    }
    /* eslint-enable no-console */
  }
};
</script>
 
<style>
.searchform {
  max-width: 300px;
  margin: auto;
}
.search-result {
  margin-top: 20px;
  text-align: left;
}
</style>