<template>
   <div id="app">
    <navbar/>
    <div class="search-text">
         <p class="text">Szukaj notatek wpisując interesujący cię przedmiot lub temat: </p>
         </div>
     <div class="search-bar">
      <b-icon-search variant="primary" font-scale="1.5"></b-icon-search>
      <input class="input" type="text"
         placeholder="Szukaj"
         v-model="filter" />
         </div>
    <div id="myTable">
     <b-table bordered 
     :items="posts"
     :fields="fields"
     :filter="filter"
      @filtered="onFiltered"
     :per-page="perPage"
    :current-page="currentPage"
     ref="table"
     class="table">
     <template #cell(actions)="data">
        <router-link class="link" :to="{ name: 'ShowPost', params: { id: data.item.materialId }}" tag="button">Przejdź</router-link>
       <router-link class="link" :to="{ name: 'EditPost', params: { id: data.item.materialId }}" tag="button">Edytuj</router-link>
       <b-button variant="outline-danger" @click="deletePost(data.item.materialId)">Usuń</b-button>
     </template>
    </b-table>

    <b-pagination
      v-model="currentPage"
      :total-rows="totalRows"
      :per-page="perPage"
      aria-controls="my-table"
      class="customPagination">
    </b-pagination>
    </div>
    <b-alert v-model="showDismissibleAlert" variant="danger" dismissible class="deleted-alert">
      Usunięto notatkę
    </b-alert>
    <Footer />
  </div>
  
</template>

<style lang="scss" scoped>
.table{
  width: 1000px !important;
  margin: auto;
  margin-top: 50px !important;
  margin-bottom: 30px;
}
.search-bar{
   width: 190px !important;
  margin: auto;
  margin-top: 20px;
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.link{
  margin-right: 20px;
}
.input{
   border: 1px solid #ddd;
}
.deleted-alert{
        margin-top: 30px !important;
        margin-bottom: 30px !important;
        width: 1000px;
        margin: auto;
    }
.search-text{
    text-align: center;
    margin-top: 30px;
    color:  #1E90FF;
  font-weight: bold;
}
div#app {
  display: flex;
  display: -webkit-flex;
  flex-direction: column;
  min-height: 100vh;
}

div#app div#myTable {
  flex-grow: 1;
}

div#app Footer {
  flex-basis: 100px;
}

.pagination{
  align-items: center;
  justify-content: center;
  margin-top: 10px;
}

</style>

<script>
// @ is an alias to /src
import navbar from '../components/Navbar.vue'
import Footer from '../components/Footer.vue'
import $ from 'jquery';

    export default {
        name: 'Home',
        components: {
            navbar, Footer
        },
        data() {
            return {
                posts: [],
                showDismissibleAlert: false,
                fields: [{key: "title", label: "Tytuł notatki"}, 
                {key: "category", label: "Przedmiot"},
                 {key: "actions", label: "Akcje"}],
                filter: '',
                perPage: 10,
                currentPage: 1,
                totalRows: 1
            }
        },
        computed: {
            postsWithActions() {
                return [
                    this.posts,
                ]
            },
        rows() {
      return this.posts.length;
    },
        },
        methods: {
            async deletePost(id) {
                $.ajax({
                    url: `https://localhost:44335/KnowledgeSharing/Delete-Post/${id}`,
                    method: 'delete'
                })
                    .done((result) => {
                        console.log(result);
                        this.showDismissibleAlert=true;
                    
                    })
                    .fail((err) => {
                        console.log(err);
                    });
            },
            onRowSelected(items) {
                this.selected = items
            },
             onFiltered(filteredItems) {
        this.totalRows = filteredItems.length
        this.currentPage = 1
      }
        },
        async created() {
            $.ajax({
                url: 'https://localhost:44335/KnowledgeSharing/All-Posts',
                method: 'get'
            })
                .done((result) => {
                    this.posts = result;
                    console.log("result");
                    this.totalRows = this.posts.length
                })
                .fail((err) => {
                    console.log(err);
                });
        },
    }
</script>
