<template>
  <div>
    <b-navbar class="navbar" toggleable="lg">
    <b-navbar-brand><h1 class="title">KNOWLEDGE SHARING</h1></b-navbar-brand>
    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
  </b-navbar>
    <b-table striped hover :items="posts"></b-table>
  </div>
</template>

<style scoped>
.navbar{
  background-color:#cc0000;
  height: 120px;
}
h1{
  color:white;
  text-align: center;
}
.title{
  font-size: 80px;
  text-align: center;
}
.navbar-brand {
    padding: 15px;
    text-align: center;
    width: 100%;
}
.footer{
  background-color: #cc0000;
  width:100%;
  height: 65px;
  bottom:0;
  margin-bottom: 0px;
  margin-top: 20px;
  color: white;
}
</style>

<script>
import $ from 'jquery';

export default {
  name: 'App',
  data(){
    return {
      posts:[]
    }
  },
   async created() {
       $.ajax({
            url: 'https://localhost:44335/api/Materials',
            method: 'get'
        })
        .done((result) => {
            this.posts = result;
            console.log("result");
        })
        .fail((err) => {
            console.log(err);
        });
    },
  methods:{
    addPost(newPost){
      this.posts = [...this.posts,newPost]
    },
    deletePost(id){
      this.posts = this.posts.filter((post) => post.id !== id)
    }
  }
};
</script>
