<template>
  <div class="my-form">
      <form class="ui form">
          <div class="fields">
              <div class="search-wrapper panel-heading col-sm-12">
                  <input class="form-control"
                    type="text" 
                    name="text search" 
                    placeholder="Text Search"
                    v-model="textSearch"
                  />
              </div>
          </div>

          <div class="fields">
              <div class="four wide field">
                  <label>First Name</label>
                  <input 
                    type="text" 
                    name="first_name" 
                    placeholder="First Name"
                    v-model="form.first_name"
                  />
              </div>

              <div class="four wide field">
                  <label>Last Name</label>
                  <input 
                    type="text" 
                    name="last_name" 
                    placeholder="Last Name"
                    v-model="form.last_name"
                  />
              </div>

              <div class="six wide field">
                  <label>Email</label>
                  <input 
                    type="email" 
                    name="email" 
                    placeholder="joe@gmail.com"
                    v-model="form.email"
                  />
              </div>

              <div class="three wide field">
                  <button :class="btnClass" @click.prevent="onFormSubmit">{{ btnSaveName }}</button>
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
          btnClass: "ui primary button submit-button",
      };
  },
  props: {
      form: {
          type: Object,
      },
      textSearch: null
  },
  methods: {
      onFormSubmit() {
          console.log(this.form)
          //form validation
          if (this.formValidation()) {
              //window.console.log("ready to tsubmit")
              this.$emit("onFormSubmit", this.form);

              console.log(this.form)

              //change the button to save 
              this.btnSaveName = "Save";
              this.btnClass = "ui primary buttn submit-button";

              //clear form fields
              this.clearFormFields();
          }
      },

      formValidation() {
          //first name
          if (this.form.first_name === "") {
              alert("Enter first name");
              return false;
          }

          //last name 
          if (this.form.last_name === "") {
              alert("Enter last name");
              return false;
          }

          //email
          if (this.form.email === "") {
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

          // clear form fields
          document.querySelector(".form").reset();
      }
  },

  updated() {
      if (this.form.isEdit) {
          this.btnSaveName = "Update";
          this.btnClass = "ui orange button submit-button";
      }
  },

}
</script>

<style scoped>

</style>
