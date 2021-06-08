<template>
    <div>
    <b-navbar class="navbar">
    <a href="/" class="navbar-brand  d-block">Knowledge Sharing</a>
      <b-navbar-nav class="items">
        <b-nav-item class="create"  :to="{name: 'Home'}" >Strona główna</b-nav-item>
        <b-nav-item class="create"  :to="{name: 'CreatePost'}" >Dodaj notatkę</b-nav-item>
      </b-navbar-nav>
  </b-navbar>
    </div>
</template>

<style scoped>
.navbar-brand {
    color:white;
    display: block;
     font-size: 50px;
     text-align: center;
     margin-right: auto !important;
     font-family: Avenir, Helvetica, Arial, sans-serif;
}
.navbar{
  background-color: #1E90FF;
  height: 100px;
  text-align: center;
}
.navbar .navbar-brand:hover, 
.navbar .navbar-brand:focus {
  background-color: transparent;
  color: white;
}
.create{
    color:white;
}
.items{
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
.navbar-light .navbar-nav .nav-link{
  color: white;
}
</style>