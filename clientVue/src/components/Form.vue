<template>
  <form class="col-lg-10">
    <div class="row">
      <div class="form-group mr-2">
        <label class="control-label">LastName</label>
        <input
          type="text"
          class="form-control"
          name="lastName"
          placeholder="Your last name"
          :value="form.lastName"
          @change="handleChange"
        />
      </div>
      <div class="form-group mr-2">
        <label class="control-label" for="idError">FirstName</label>
        <input
          type="text"
          class="form-control"
          name="firstName"
          placeholder="Your first name"
          :value="form.firstName"
          @change="handleChange"
        />
      </div>
      <div class="form-group mr-2">
        <label class="control-label" for="idError">Email</label>
        <input
          type="email"
          class="form-control"
          name="email"
          placeholder="gmail@gmail.com"
          :value="form.email"
          @change="handleChange"
        />
      </div>
      <div class="form-group mr-2">
        <div style="height: 30px" class="col-lg-1"></div>

        <button type="submit" v-if="form.isEdit" class="btn btn-primary" @click="onFormModif">Save</button>
        <button type="submit" v-if="!form.isEdit" class="btn btn-info" @click="onFormSubmit">Create</button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  name: "Form",
  props: {
    form: {
      type: Object
    }
  },
  methods: {
    handleChange(event){
      const { name, value } = event.target
      let form = this.form
      form[name] = value
      //this.form = form
    },
    onFormSubmit(e){
      e.preventDefault()

      if(this.formValidation()){
        this.$emit("onFormSubmit", this.form);
      }
    },
    onFormModif(e){
      e.preventDefault()

      if(this.formValidation()){
        this.$emit("onFormSave", this.form);
      }
    },
    formValidation(){
      //first name
      if(document.getElementsByName("firstName")[0].value===""){
        alert("Enter firstName");
        return false
      }
      //last name
      if(document.getElementsByName("lastName")[0].value===""){
        alert("Enter LastName");
        return false
      }
      //email
      if(document.getElementsByName("email")[0].value===""){
        alert("Enter email");
        return false
      }
      return true
    }
  }
};
</script>

<style>
</style>