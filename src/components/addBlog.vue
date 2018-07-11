<template>
  <div id="add-blog">
    <h2>Add a new Blog Post</h2>
    <form v-if="!submited">
      <label>Blog Title:</label>
      <input type="text" v-model.lazy="blog.title" required>
      <label>Blog Content:</label>
      <textarea v-model.lazy="blog.content"></textarea>
      <div id="checkboxes">
        <label>Lion Man</label>
        <input type="checkbox" value="lion" v-model="blog.categories">
        <label>Jaguar</label>
        <input type="checkbox" value="jaguar" v-model="blog.categories">
        <label>Joe Tiger</label>
        <input type="checkbox" value="tiger" v-model="blog.categories">
        <label>White Lion Man</label>
        <input type="checkbox" value="white" v-model="blog.categories">
      </div>
      <label>Author:</label>
      <select v-model="blog.author">
        <option v-for="author in authors">{{ author }}</option>
      </select>
      <button @click.prevent="post">Add Blog</button>
    </form>

    <div v-if="submited">
      <h3>Thanks for adding your post</h3>
    </div>

    <div id="preview">
      <h3>Preview Blog</h3>
      <p>Blog Title:{{ blog.title }} </p>
      <p>Blog Content {{ blog.content }}</p>
      <p>Blog Categories</p>
      <ul>
        <li v-for="category in blog.categories">{{ category }}</li>
      </ul>
      <p>Author: {{ blog.author }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      blog: {
        title: '',
        content: '',
        categories: [],
        author: ''
      },
      authors: ['Alan Moore', 'Camus', 'Kafka'],
      submited: false
    }
  },
  methods: {
      post:function(){
        this.$http.post('https://jsonplaceholder.typicode.com/posts', {
          title: this.blog.title,
          content: this.blog.content,
          userID: 1
        }).then(function(data){
          console.log(data);
          this.submited = true;
        });
      }
  }
}
</script>

<style>
  #add-blog *{
      box-sizing: border-box;
  }
  #add-blog{
      margin: 20px auto;
      max-width: 500px;
  }
  label{
      display: block;
      margin: 20px 0 10px;
  }
  input[type="text"], textarea{
      display: block;
      width: 100%;
      padding: 8px;
  }
  #preview{
      padding: 10px 20px;
      border: 1px dotted #ccc;
      margin: 30px 0;
  }
  h3{
      margin-top: 10px;
  }
  #checkboxes input{
      display: inline-block;
      margin-right: 10px;
  }
  #checkboxes label{
      display: inline-block;
  }

</style>
