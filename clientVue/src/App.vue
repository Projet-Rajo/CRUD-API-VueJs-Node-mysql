<template>
  <div class="container">
    <h1>CRUD APP</h1>
    <Form 
      :form="form" 
      @onFormSubmit="onFormSubmit"
      @onFormSave="onFormSave"
      />
    <br>
    <Loader v-if="loader"/>
    <MemberList 
      :memberList="memberList" 
      @onDeleteApp="onDeleteApp"
      @onEdit="onEdit"
      />
</div>

</template>

<script>
import axios from "axios"
import Form from "./components/Form"
import MemberList from './components/MemberList'
import Loader from './components/Loader'

export default {
  name: 'App',
  components: {
    Form,
    MemberList,
    Loader,
  },
  data(){
    return{
      url: "http://localhost:3001/api",
      memberList: [],
      form: {lastName:"", firstName:"", email:"", isEdit: false},
      loader: false,
      id:0
    }
  },
  methods: {
    getMembers(){
      this.loader = true
      axios.get(this.url+"/get").then(data => {
        this.memberList = data.data
        this.loader = false
      })
    },
    onDeleteApp(id){
      //console.log("App delete "+id)
      axios.delete(this.url+"/delete/"+id);
      this.getMembers();
    },
    onFormSubmit(data){
      //console.log("App onFormSubmit ",data)
      if(!data.isEdit){
        axios.post(this.url+"/insert", {
          lastName: data.lastName,
          firstName: data.firstName,
          email: data.email
        });
        this.getMembers();
        this.form = {lastName:"", firstName:"", email:"", isEdit: false}
      }
    },
    onFormSave(data){
      //console.log("App onFormSave ",data)
      if(data.isEdit && this.id!==0){
          //console.log(data)
          //console.log(this.id)
        axios.put(this.url+"/update", {
          lastName: data.lastName,
          firstName: data.firstName,
          email: data.email,
          id: this.id
        });
        this.getMembers();
        this.form = {lastName:"", firstName:"", email:"", isEdit: false}
        this.id = 0
      }
    },
    onEdit(data){
      //console.log("app oneEdit", data)
      this.form.lastName = data.lastName
      this.form.firstName = data.firstName
      this.form.email = data.email
      this.form.isEdit = true
      this.id = data.id
    }
  },
  created(){
    this.getMembers();
  }
}
</script>

<style>
</style>