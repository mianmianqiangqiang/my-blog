<template>
	<div id="single-blog">
	<h1>{{blog.title}}</h1>
	<article>{{blog.content}}</article>
	<p>作者：{{blog.author}}</p>
	
	<ul>
		<li v-for="category in blog.categories">
			{{category}}
		</li>
	</ul>
	<button @click="deleteSingleBlog">删除</button>
	<router-link :to="'/edit/'+id">编辑</router-link>
	</div>
</template>

<script>
	export default {
		name: "single-blog",
		data() {
			return {
				id: this.$route.params.id,
				blog: {}
			}
		},
		created() {
			this.$http.get('https://my-blog-96629.firebaseio.com/posts/' + this.id+".json")
			.then(function(data) {
//				this.blog = data.body;
                        return data.json();
			})
			.then(function(data){
				this.blog=data;
			})

		},
		methods:{
			deleteSingleBlog(){
				this.$http.delete('https://my-blog-96629.firebaseio.com/posts/' + this.id+".json")
			.then(response=>{
				this.$router.push({path:'/'})
			})
			}
		}

	}
</script>

<style>
#single-blog{
	max-width: 960px;
	margin: 0 auto;
	padding: 20px;
	background:#EEEEEE;
	border: 1px dotted #aaa;
}
</style>