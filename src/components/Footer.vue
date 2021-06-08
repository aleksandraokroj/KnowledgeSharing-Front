<template>
    <div>
        <v-footer padless class="footer">
        <v-col
      class="text-center"
      cols="12">
      Projekt stworzony przez: Aleksandra Okrój, Natalia Skórowska - <strong>{{ new Date().getFullYear() }}</strong>
    </v-col>
  </v-footer>
    </div>
</template>

<style scoped>
.footer{
    margin-top: 50px;
    margin-bottom: 0px;
    bottom:0;
    background-color: #1E90FF;
    color: white;
    height: 60px;
}
</style>
