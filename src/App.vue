<template>
<div class="container">
<div class="row">
    <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
    <h1>Http</h1>
        <div class="form-group">
          <label for="user">username:</label>
          <input type="text" id="user" class="form-control" v-model="user.username">
        </div>
        <div class="form-group">
          <label for="email">email:</label>
          <input type="text" id="email" class="form-control" v-model="user.email">
        </div>

        <button type="submit" @click="submit">Login</button>
        <hr>
        <button type="submit" @click="fetchData">Get Data</button>
        <hr>
        <br>

        <ul class="list-group">
          <li class="list-group-item" v-for="u in users" :key="u.email">{{ u.email }}</li>
        </ul>
  </div>
  </div>
</div>
</template>

<script>
export default {
  data() {  
    return {
      user: {
        username: '',
        email: ''
      },
      users: []
    };
},
  methods: {
    submit() {
      console.log(this.user);
      this.$http.post('data.json', this.user)
        .then(response => {
            console.log(response);
        }, error => {
            console.log(error);
        })
  },
  fetchData() {
    this.$http.get('data.json')
        .then(response => {
          return response;
        })
        .then(data => {
          console.log(data.body);
          const resultArray = [];
          for (let key in data.body){
            console.log(data.body[key]);
            //const item = data.body[key];
            resultArray.push(data.body[key]);
          }
          this.users = resultArray;
          console.log(this.users);
          console.log(this.users[0].email);

        })
  }
}
}
</script>

<style>
</style>
