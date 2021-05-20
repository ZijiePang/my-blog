<template>
    <div id="single-blog">
        <h1>{{blog.title}}</h1>
        <article>{{blog.content}}</article>
        <p>Author: {{blog.author}}</p>
        <p>Categories:</p>
        <ul>
            <li v-for="category in blog.categories" v-bind:key='category'>
                {{category}}
            </li>
        </ul>
    </div>
</template>

<script>
/* 路由参数，可以根据网页输入框地址而显示相对id的数据 */
export default {
    name:"single-blog",
    data(){
        return{
            id: this.$route.params.id,
            blog:{},
        }
    },
    created(){
        this.$http.get(`https://my-blog-vue-c1d83-default-rtdb.firebaseio.com/posts/`+ this.id + ".json")
        .then(function(data){
            return data.json();
        })
        .then(function(data){
            this.blog = data;
        })
    },
}
</script>

<style scoped>
#single-blog{
    max-width: 960px;
    margin: 0 auto;
    padding: 20px;
    background: #eee;

}
</style>