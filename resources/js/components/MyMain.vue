<template>

    <div class='container'>
        <div v-if="loding" class="d-flex justify-content-center">
            <div class="spinner-border" role="status">
            <span class="visually-hidden">Loading...</span>
           
        </div>
    </div> 

  <div v-else class="card mb-5 mt-5" v-for="(post,index) in posts" :key="index">

    <div class="card-body ">
    <h2 clss="card-title">{{post.title}}</h2>
    <h5 clss="card-title">{{post.slug}}</h5>
    <p class="card-text">{{troncaText(post.content,150)}}</p>
    <p class="card-text">{{post.category?post.category.name:'-'}}</p>

    <a href="" class="btn btn-primary" >Read more...</a>

    </div>
    
  </div>
   <nav >
    <ul class="pagination">
    <li class="page-item"><a class="page-link" href="#">Previous</a></li>
    <li class="page-item"><a class="page-link" href="#">Next</a></li>
    </ul>
   </nav>
</div>




</template>

<script>
    export default {
            name:'MyMain',
            data(){
                return{
                    posts:[], 
                    loding: true,
                    paginaCorrente: 1,
                    ultmaPagina:null,
                }

            },
            methods:{
                getPosts(){
                    this.loding = true
                    axios.get('/api/posts')
                    .then((response)=>{
                       this.posts= response.data.results.data;
                       this.loding = false
                       this.paginaCorrente = response.data.results.current_page;
                       this.ultmaPagina = response.data.results.last_page;
                    });
                },
                troncaText(text,lungezza ){
                    if(text.length < lungezza){
                        return text;
                    }else{
                    return text.substring(0,lungezza) + '...';

                    }
                    
                }
            },
            mounted(){
                this.getPosts();
            },
    }
</script>

<style>

</style>