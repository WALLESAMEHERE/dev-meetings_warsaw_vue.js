<template>
  <div id="app">
    <h1>List from api > https://jsonplaceholder.typicode.com/users</h1>
    <form @submit.prevent="onSubmit()">
      <label>Name</label><input type="text" placeholder="name" v-model="newUser.name">
      <label>Nickaname</label><input type="text" placeholder="nick" v-model="newUser.username">
      <label>e-mail</label><input type="text" placeholder="e-mail" v-model="newUser.email">
      <label>phone</label><input type="text" placeholder="number" v-model="newUser.phone">
      <button type="submit">Add user</button>
    </form>
    <label>Filter by</label><button @click="filterName">Name</button><button >e-mail</button><button >Nickname</button>
    <ul>
      <li v-for="(p,index) in results">{{ p.email }}, {{ p.name }}, {{ p.username }}<button @click="removeUser(index)">x</button></li>
    </ul>

  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'app',
   data(){
      return {
          results: [],
          newUser: {
            name: '',
            username: '',
            email: '',
            phone: ''
          }
      }
    },
        mounted() {
          axios.get('https://jsonplaceholder.typicode.com/users').then(response => {
            this.results = response.data;
            console.log(this.results);
          })
        },
        methods:{
            onSubmit(){
                this.results.push({
                  ...this.newUser
                });
                this.newUser = {};
            },
            removeUser(index){
              this.results.splice(index,1)
            },
            filterName(){
              this.results.sort((a,b) => {
                return a.name -b.name
              })
            }
         }

  }
</script>

<style>
*{
  text-align: center;
}
form{
  padding: 5px;
  margin: 20px;
  border: 2px solid grey;
}
input{
  margin: 2px;
}
ul{
  list-style-type: none;
}
</style>
