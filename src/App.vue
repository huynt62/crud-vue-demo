<template>
  <div id="app">
    <div class="ui fixed inverted menu vue-color">
      <div class="ui container">
        <a href="#" class="header item">Vue JS CRUD</a>
      </div>
    </div>

    <div class="ui main container">
      <MyForm :form="form" @onFormSubmit="onFormSubmit" />
      <Loader v-if="loader" />
      <CustomerList 
        :customers="customers"
        @onDelete="onDelete"
        @onEdit="onEdit"
      />
    </div>
  </div>
</template>

<script>
//import axios from "axios";
import MyForm from "./components/MyForm";
import CustomerList from "./components/CustomerList";
import Loader from "./components/Loader";

export default {
  name: 'App',
  components: {
    MyForm,
    CustomerList,
    Loader
  },
  data() {
    return {
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
      form: { first_name: "", last_name: "", email: "", isEdit: false },
      loader: false
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

      this.loader = false;
    },
    editCustomer(data) {
      this.loader = true;
      console.log(this.customers[this.customers.indexOf(data.id)])
      var customer1 = {
        id: data.id,
        first_name: data.first_name,
        last_name: data.last_name,
        email: data.emai
      };
    
      console.log(this.customers[this.customers.indexOf(data.id)])
      this.customers[this.customers.indexOf(data.id)] = customer1;
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

    onSearch(id) {

      var search1 = this.form;
      console.log(id)
      console.log(search1)
      for ( var i = 1; i < this.customers.length; i++ ) {
        if(this.customers[i].id === id) {
          search1.id = this.customers[i].id;
          search1.first_name = this.customers[i].first_name;
          search1.last_name = this.customers[i].last_name;
          search1.email = this.customers[i].email;
        }
      }
      console.log(search1)
      alert("Name: " + search1.first_name + " " + search1.last_name
        + "\nEmail: " + search1.email
      );
    }
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
