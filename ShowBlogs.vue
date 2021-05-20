<template>
  <div id="show-blogs">
      <input type="text" v-model="search" placeholder="Search">

      <h1>Menu</h1>
      <div v-for="blog in filteredBlogs" v-bind:key="blog.id" class="single-blog">
          <router-link :to="'/blog/' + blog.id">
            <h2>{{blog.title | to-uppercase}}</h2>
            <article>{{blog.content | snippet}}</article>
          </router-link>
      </div>
     
    
  </div>
</template>

<script>

export default {
  name:'show-blogs',
  data(){
      return{
          blogs:[],
          search:"",
      }

  },
  created(){
      this.$http.get("https://my-blog-vue-c1d83-default-rtdb.firebaseio.com/posts.json")
      .then(function(data){
          //this.blogs = data.body;
          return data.json()
      })
      .then(function(data){
          var blogsArray = [];
          for (let key in data){
              data[key].id = key;
              blogsArray.push(data[key]);
          }
          this.blogs = blogsArray
      })
  },
  computed:{ 
      filteredBlogs:function(){
          return this.blogs.filter((blog)=>{
              return blog.title.match(this.search);
          })
      }
  }
}
</script>

<style>
#show-blogs{
    max-width: 800px;
    margin: 0 auto;
}
#show-blogs a{
    color: #444;
    text-decoration: none;
}
input[type='text']{
    padding: 8px;
    width: 100%;
    box-sizing: border-box;
}

.single-blog{
    padding: 20px;
    margin: 20px 0;
    box-sizing: border-box;
    background: #eee;
    
}

</style>
