<template>
<div>
        <br>
        <br><br>
        <form @submit="addPost">
        <div class="form-group">
            <input required type="text" v-model="title" placeholder="treść" name="title" id="" class="form-control">
        </div>
        <div class="form-group">
            <button class="btn btn-block btn-danger">
                Dodaj
            </button>
        </div>
        </form>
    </div>
</template>
<script>

export default {
  name: "AddPost",
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addPost(e) {
        e.preventDefault()
      const newPost = {
        id:Date.now(),
        title: this.title,
      }
      // Send up to parent
      this.$emit('add-post', newPost);
      this.title = '';
    }
  }
}
</script>

<style scoped>
</style>