<template>
  <div class="my-form">
      <form class="ui form">
          <div class="fields">
              <div class="three wide field">
                  <input 
                    type="text" 
                    name="id" 
                    placeholder="ID"
                    @change="handleChange"
                    :value="form.id"
                  />
              </div>
              <div class="tow wide field">
                  <button class="ui primary button search-button" @click="onSearch">Search</button>
              </div>
          </div>
          <div class="fields">
              <div class="four wide field">
                  <label>First Name</label>
                  <input 
                    type="text" 
                    name="first_name" 
                    placeholder="First Name"
                    @change="handleChange"
                    :value="form.first_name"
                  />
              </div>

              <div class="four wide field">
                  <label>Last Name</label>
                  <input 
                    type="text" 
                    name="last_name" 
                    placeholder="Last Name"
                    @change="handleChange"
                    :value="form.last_name"
                  />
              </div>

              <div class="six wide field">
                  <label>First Name</label>
                  <input 
                    type="email" 
                    name="email" 
                    placeholder="joe@gmail.com"
                    @change="handleChange"
                    :value="form.email"
                  />
              </div>
              
              <div class="three wide field">
                  <button :class="btnClass" @click="onFormSubmit">{{ btnSaveName }}</button>
              </div>
          </div>
      </form>
  </div>
</template>

<script>
export default {
  name: 'MyForm',
  data() {
      return {
          btnSaveName: "Save",
          btnClass: "ui primary button submit-button"
      };
  },
  props: {
      form: {
          type: Object
      }
  },
  methods: {
      handleChange(event) {
          const { name, value } = event.target;
          let form = this.form;
          form[name] = value;
          this.form = form;
      },

      onSearch(event) {
          //prevent search
          event.preventDefault();

          if (document.getElementsByName("id")[0].value === "") {
              alert("Enter id");
          }
      },

      onFormSubmit(event) {
          //prevent form submit
          event.preventDefault();

          //form validation
          if (this.formValidation()) {
              //window.console.log("ready to tsubmit")
              this.$emit("onFormSubmit", this.form);

              //change the buttn to save 
              this.btnSaveName = "Save";
              this.btnClass = "ui primary buttn submit-button";

              //clear form fields
              this.clearFormFields();
          }
      },

      formValidation() {
          //first name
          if (document.getElementsByName("first_name")[0].value === "") {
              alert("Enter first name");
              return false;
          }

          //last name 
          if (document.getElementsByName("last_name")[0].value === "") {
              alert("Enter last name");
              return false;
          }

          //email
          if (document.getElementsByName("email")[0].value === "") {
              alert("Enter email");
              return false
          }

          return true;
      },
      clearFormFields() {
          //clear form data
          this.form.first_name = "";
          this.form.last_name = "";
          this.form.email = "";
          this.form.isEdit = false;

          //clear form fields
          document.querySelector(".form").reset();
      }
  },

  updated() {
      if (this.form.isEdit) {
          this.btnSaveName = "Update";
          this.btnClass = "ui orange button submit-button";
      }
  }

}
</script>

<style scoped>

</style>
