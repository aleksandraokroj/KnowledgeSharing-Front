<template>
    <div class="app">
        <navbar/>
        <div>
        <b-card
        :footer="footerText"
        class="card">
        <template #header>
        <h1 class="title">{{post.title}}</h1>
        </template>
        <b-text class="content">{{post.content}}</b-text>
        </b-card>
        </div>
       
    </div>
</template>

<style lang="scss" scoped>
.card{
    width: 1000px;
    margin-top: 50px !important;
    align-content: center;
    margin: 0 auto; /* Added */
    float: none; /* Added */
}
.app{
        font-family: Avenir, Helvetica, Arial, sans-serif;
    }
.content{
    letter-spacing: 1px;
    text-align: justify;
}
.title{
    color: 	#1E90FF;
        font-size: 50px;
        text-transform: uppercase;
        text-align: center;
        padding: 30px;
        font-weight: 700;
}
.card-footer{
        text-align: right;
    }
</style>

<script>
import navbar from '../components/Navbar.vue';
import $ from 'jquery';
export default ({
    name:'Post',
    components:{navbar},
    computed: {
            footerText(){
                return 'Autor: ' + this.post.userInfo
            }
        },
     data(){
    return {
      post: {},
    }
  },
     async created() {
       $.ajax({
            url: 'https://localhost:44335/KnowledgeSharing/Post/'+this.$route.params.id,
            method: 'get'
        })
        .done((result) => {
            this.post = result;
            console.log("result");
        })
        .fail((err) => {
            console.log(err);
        });
    },
})
</script>
