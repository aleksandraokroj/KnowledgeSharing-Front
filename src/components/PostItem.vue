<template>
  <div class="container">
    <div class="post-item" v-bind:class="{'is-complete':post.completed}">
      <p>
        <input type="checkbox" v-on:change="markComplete" v-bind:checked="post.completed" />
        {{post.title}}
        <button class="update" @click="updatePost">Modyfikuj</button>
        <button @click="$emit('del-post', post.id)" class="del">x</button>
      </p>
    </div>
    <div v-if="this.flag">
      <form @submit="updatePostMethod">
        <div class="form-group">
          <input
            class="form-control"
            v-model="updateTitle"
            type="text"
            :placeholder="title"
            name
            id
          />
        </div>
        <div class="form-group">
          <button class="btn btn-danger">Modyfikuj</button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "PostItem",
  props: ["post", "posts", "title", "id"],
  methods: {
    markComplete() {
      this.post.completed = !this.post.completed;
    },
    updatePost() {
      this.flag = !this.flag;
    },
    updatePostMethod(e) {
      e.preventDefault();
      console.log(this.title);
      console.log(this.id);
      this.posts.filter((post) => {
        if (post.id == this.id) {
          post.title = this.updateTitle;
        }
      });
      this.flag = false
    },
  },
  data() {
    return {
      flag: false,
      updateTitle: "",
    };
  },
};
</script>

<style scoped>
.post-item {
  background: #f4f4f4;
  padding: 10px;
  margin: 20px;
  border-bottom: 1px #ccc dotted;
}
.is-complete {
  text-decoration: line-through;
}
.del {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
.update {
  background: green;
  color: #fff;
  border: none;
  padding: 5px 9px;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>