<template>
    <div class="container mt-3">
        <div class="card p-3 text-center">
            <div class="d-flex flex-row justify-content-center mb-3">
                <div class="image"> <img src="../img.jpg" style="width:150px ; height:150px" class="rounded-circle"> <span><i class='bx bxs-camera-plus'></i></span> </div>
            </div>
            <h4>Edit Profile</h4>
            <div class="row">
                <div class="col-md-6">
                    <div class="inputs"> <label>First Name</label> <input v-model="first_name"  class="form-control" type="text"> </div>
                </div>
                <div class="col-md-6">
                    <div class="inputs"> <label>Last Name</label> <input v-model="last_name"  class="form-control"  type="text" placeholder="Last Name"> </div>
                </div>
                <div class="col-md-6">
                    <div class="inputs"> <label>Address</label> <input v-model="address"   class="form-control"  type="text" placeholder="Address"> </div>
                </div>
                <div class="col-md-6">
                    <div class="inputs"> <label>Telefon</label> <input v-model="telefon"  class="form-control"  type="text" placeholder="Telefon"> </div>
                </div>
            </div>
            
            <div class="mt-3 gap-2 d-flex justify-content-end"> <button @click="updateProfile" class="px-3 btn btn-sm btn-primary">Save</button> </div>
            
        </div>
        <h3 v-if="hide===false">Updated Successfully</h3>
    </div>
</template>




<script>
import {reactive} from "vue"
import axios from 'axios'
import { useRouter } from "vue-router";
export default {
  data() {
    return {
      first_name:'',
      last_name:'',
      address:'',
      telefon:'',
      error:'ERRORRRR',
      hide: true
    };
  },
  mounted() {
    axios.get('http://localhost:8000/jobs/api/profile',{withCredentials:true})
      .then(response => {
        this.first_name = response.data.profile.first_name;
        this.last_name = response.data.profile.last_name;
        this.address = response.data.profile.address;
        this.telefon = response.data.profile.telefon;
      })
      .catch(error => {
        this.error = error.message;
      });
     },
     methods: {
      updateProfile(){
           axios.patch('http://localhost:8000/jobs/api/profileupdate', { first_name: this.first_name,
           last_name: this.last_name,
           address:this.address,
           telefon:this.telefon}, { withCredentials: true }).then(response => console.log(response.data), this.hide= false)
      }
     },

};
</script>