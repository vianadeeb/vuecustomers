<template>
  <div class="details container">
    <router-link to="/">Back</router-link>
     <br/>
    <h1 class="page-header">{{customer.first_name}} {{customer.last_name}}
        <span class="pull-right">  <br/>
            <router-link class="btn btn-primary" v-bind:to="'/edit/'+customer.id">Edit</router-link>
            <button class="btn btn-danger" v-on:click="deleteCustomer(customer.id)">Delete</button>
            </span>
    </h1>
    <br/>  <br/>  <br/>  <br/>
    <ul class="list-group">
            <li class="list-group-item"><span class="glyphicon glyphicon-phone" aria-hidden="true"></span> {{customer.email}}</li>
            <li class="list-group-item"><span class="glyphicon glyphicon-envelope" aria-hidden="true"></span> {{customer.email}}</li>
        </ul>

        <ul class="list-group">
            <li class="list-group-item"> {{customer.email}}</li>
            <li class="list-group-item">{{customer.first_name}}</li>
            <li class="list-group-item">{{customer.last_name}}</li>
        </ul>
  </div>
</template>

<script>
export default {
  name: 'customerdetails',
  data () {
    return {
      customer: ''
    }
  },
  methods:{
      fetchCustomer(id){
          this.$http.get('https://reqres.in/api/users?page=2'+id)
          .then(function(response){
            this.customer = response.body;
          });
      },
      deleteCustomer(id){
          this.$http.delete('https://reqres.in/api/users/2'+id)
          .then(function(response){
            this.$router.push({path: '/', query: {alert: 'Customer Deleted'}});
          });
      }
  },
  created: function(){
      this.fetchCustomer(this.$route.params.id);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
