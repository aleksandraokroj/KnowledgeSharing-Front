<template>
    <div id="app">
        <navbar/>
         <div id = "error">
        <center >
            <h2>Błąd 404</h2>
            <h2>Nie znaleziono tej strony na naszym serwerze</h2>
        </center>
    </div>
        <Footer/>
    </div>
</template>

<style
>
div#app {
  display: flex;
  display: -webkit-flex;
  flex-direction: column;
  min-height: 100vh;
}

div#app div#error {
  flex-grow: 1;
}

div#app Footer {
  flex-basis: 100px;
}

div#error {
    margin-top: 200px;
}
</style>

<script>
import  navbar from "../components/Navbar.vue";
import Footer from '../components/Footer.vue'
export default {
    name:'ErrorPage',
    components: {
        navbar, Footer
    }
}
</script>