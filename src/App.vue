<template>
  <div id="app">
    <div class="ui fixed inverted menu vue-color">
      <div class="ui container">
        <a href="#" class="header item">Vue JS CRUD</a>
      </div>
    </div>

    <div class="ui main container">
      <MyForm
        :form="form" 
        :textSearch="textSearch"
        @onSearch="onSearch"
        @onFormSubmit="onFormSubmit"
      />
      <Loader v-if="loader" />
      <CustomerList 
        :onSearch="onSearch"
        @onDelete="onDelete"
        @onEdit="onEdit"
      />
      <View/>
    </div>
  </div>
</template>

<script>
//import axios from "axios";
import MyForm from "./components/MyForm";
import CustomerList from "./components/CustomerList";
import Loader from "./components/Loader";
//import Vue from 'vue';

export default {
  name: 'App',
  components: {
    MyForm,
    CustomerList,
    Loader
  },
  data() {
    return {
      textSearch: null,
      customers: [
        {id: 1, first_name: 'Nguyen Van', last_name: 'A', email: 'emailA@gmail.com'},
        {id: 2, first_name: 'Nguyen Van', last_name: 'B', email: 'emailB@gmail.com'},
        {id: 3, first_name: 'Nguyen Van', last_name: 'C', email: 'emailC@gmail.com'},
        {id: 4, first_name: 'Nguyen Van', last_name: 'D', email: 'emailD@gmail.com'},
        {id: 5, first_name: 'Nguyen Van', last_name: 'D', email: 'emailD@gmail.com'},
        {id: 6, first_name: 'Nguyen Van', last_name: 'D', email: 'emailD@gmail.com'},
        {id: 7, first_name: 'Nguyen Van', last_name: 'D', email: 'emailD@gmail.com'},
        {id: 8, first_name: 'Nguyen Van', last_name: 'D', email: 'emailD@gmail.com'},
        {id: 9, first_name: 'Nguyen Van', last_name: 'D', email: 'emailD@gmail.com'},
        {id: 10, first_name: 'Nguyen Van', last_name: 'D', email: 'emailD@gmail.com'},
        {id: 11, first_name: 'Nguyen Van', last_name: 'D', email: 'emailD@gmail.com'},
        {id: 12, first_name: 'Nguyen Van', last_name: 'D', email: 'emailD@gmail.com'},
        {id: 13, first_name: 'Nguyen Van', last_name: 'D', email: 'emailD@gmail.com'},
      ],
      form: {first_name: "", last_name: "", email: "", isEdit: false},
      loader: false,
    }
  },

  computed:{
    onSearch() {
      /*console.log(this.textSearch)
      console.log(this.customers.filter((item)=>{
        return this.textSearch.toLowerCase().split(' ').every(v => 
              item.first_name.toLowerCase().includes(v)||
              item.last_name.toLowerCase().includes(v) ||
              item.email.toLowerCase().includes(v) 
            )
      }))*/
      console.log(typeof(this.textSearch))

      if(this.textSearch){
      return this.customers.filter((item)=>{
        return this.textSearch.toLowerCase().split(' ').every(v => 
              item.first_name.toLowerCase().includes(v)||
              item.last_name.toLowerCase().includes(v) ||
              item.email.toLowerCase().includes(v) 
            )
      })
      }else{
        return this.customers;
      }
    }
  },

  methods: {
    deleteCustomer(id) {
      this.loader = true;

      var filter1 = [];
      filter1 = this.customers.filter(obj => obj.id !== id);
      this.customers = filter1;

      this.loader = false;
    },
    createCustomer(data) {
      this.loader = true;

      this.customers.push({
          id: this.customers[this.customers.length - 1].id +1,
          first_name: data.first_name,
          last_name: data.last_name,
          email: data.email
      });
      console.log(this.customers)

      this.loader = false;
    },
    editCustomer(data) {
      this.loader = true;

      var customer1 = {
        id: Number(data.id),
        first_name: String(data.first_name),
        last_name: String(data.last_name),
        email: String(data.email)
      }

      for(var i = 0; i < this.customers.length; i ++) {
        if(this.customers[i].id === customer1.id) {
          //should not used:  this.customers[i] = customer1;
          this.customers.splice(i,1,customer1);
          break;
        }
      }
      this.loader = false;
    },
    onDelete(id) {
      // window.console.log("app delete " + id);
      this.deleteCustomer(id);
    },
    onEdit(data) {
      // window.console.log("app edit ", data);
      this.form = data;
      this.form.isEdit = true;
    },
    onFormSubmit(data) {
      // window.console.log("app onFormSubmit", data);

      if (data.isEdit) {
        // call edit customer
        this.editCustomer(data);
      } else {
        // call create customer
        this.createCustomer(data);
      }
    },
  },
};
</script>

<style>
.vue-color {
  background: #41b883 !important;
}

.main.container {
  margin-top: 60px;
}

.submit-button {
  margin-top: 24px !important;
  float: right;
}

.data {
  margin-top: 15px;
}

thead tr th {
  background: #e0e0e0 !important;
}

.ui.inverted.dimmer {
  background-color: rgba(255, 255, 255, 0) !important;
}
</style>
