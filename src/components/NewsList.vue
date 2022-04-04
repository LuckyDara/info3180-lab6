<template>
    <form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
        <div class="input-group mx-sm-3 mb-2">
            <label class="visually-hidden" for="search">Search</label>
            <input type="search" name="search" v-model="searchTerm" id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter search term here" />
            <button class="btn btn-primary mb-2">Search</button>
        </div>
        <p>You are searching for {{ searchTerm }}</p>
    </form>
    <ul class="news__list">
          <li v-for="article in articles" class="news__item">
              <div class="card" style="width:18 rem">
                  <img class="card-img-top" :src='article.urlToImage' alt="Card image cap"/>
                  <div class="card-body">
                      <h5 class="card-title" style="font-weight:600">{{ article.title }}</h5>
                      <p class="card-text">{{ article.description }}</p>
                    </div>
                </div>
            </li>
    </ul>
</template>
<script>
    export default {
        data() {
            return {
                articles:[],
                searchTerm: ''
               
            };
        },
        methods: {
            searchNews() {
                let self = this;
                fetch('https://newsapi.org/v2/everything?q='+
                self.searchTerm + '&language=en', {
                    headers: {
                    'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
                    }
                })
                .then(function(response) {
                    return response.json();
                })
                .then(function(data) {
                    console.log(data);
                    self.articles = data.articles;
                });
            }
        },
        
        created() {
            let self = this;
            fetch('https://newsapi.org/v2/top-headlines?country=us',
            {
                headers: {
                    'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
                    }
            })
            .then(function(response) {
                 return response.json();
            })
            .then(function(data) {
                console.log(data);
                self.articles = data.articles;
            });
        }
    };
</script>

<style>
.news__item img{
    width: 100% !important;
}
.news__item{
    width: 350px !important;
    
}
.card{
    border-style: none;
    border-bottom: 3px solid lightseagreen;
    height: 600px;
    margin-bottom: 10%;
    box-shadow: 0px -3px 10px 3px rgb(196, 196, 196);
}
.card-body{
    text-align: left;
}
.news__list{
    list-style:none;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-evenly;
    margin-top: 10%;
}
</style>